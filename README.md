# SR-FLIPFLOP-

Design code:

module sr_flipflop (
    input s,     
    input r,     
    input clk,   
    output reg q,
    output qn    
);

    assign qn = ~q;  

    always @(posedge clk) begin
        if (s && ~r) begin
            q <= 1'b1;  
        end 
        else if (~s && r) begin
            q <= 1'b0;  
        end 
        else if (s && r) begin
            q <= 1'b0; 
        end   
    end

endmodule

Test bench:

module sr_flipflop_tb();
    reg s, r, clk;  
    wire q, qn;     
    sr_flipflop uut (
        .s(s),
        .r(r),
        .clk(clk),
        .q(q),
        .qn(qn)
    );
    initial begin
        clk = 0;
        forever #5 clk = ~clk;  
    end
    initial begin
        s = 0; r = 0;
        #10;
        s = 1; r = 0;
        #10;
        s = 0; r = 1;
        #10;
        s = 1; r = 1;
        #10;
        s = 0; r = 0;
        #10;
        s = 1; r = 0;
        #10;
        s = 0; r = 1;
        #10;
        s = 0; r = 0;
        #10;
        $stop;
    end
    initial begin
        $monitor("At time %0t: s=%b r=%b q=%b qn=%b", $time, s, r, q, qn);
    end
endmodule

