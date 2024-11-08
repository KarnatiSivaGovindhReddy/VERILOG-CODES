# VERILOG-CODES
# 3X3 MULTIPLIER
# GATE LEVEL MODELLING CODE
module multiplier_gate_level(
    input [2:0] A, 
    input [2:0] B, 
    output [5:0] P 
);
    wire [5:0] temp; 
    assign temp[0] = A[0] & B[0];
    assign temp[1] = (A[1] & B[0]) ^ (A[0] & B[1]);
    assign temp[2] = (A[2] & B[0]) ^ (A[1] & B[1]) ^ (A[0] & B[2]);
    assign temp[3] = (A[2] & B[1]) ^ (A[1] & B[2]);
    assign temp[4] = A[2] & B[2];
    assign temp[5] = 0; // No carry-out
    assign P = temp;
endmodule
# DATA FLOW MODELING CODE
module multiplier_data_flow(
    input [2:0] A,
    input [2:0] B,
    output [5:0] P 
);
    assign P = A * B;
endmodule
# TEST BENCH CODE
module testbench;
    reg [2:0] A;           
    reg [2:0] B;           
    wire [5:0] P;          
    multiplier_data_flow uut (
        .A(A),
        .B(B),
        .P(P)
    );
    initial begin
        // Test case: A = 111 (7 in decimal), B = 011 (3 in decimal)
        A = 3'b111;         
        B = 3'b011;         
        #10;                
        $display("Test Case: A = %b, B = %b, Product (P) = %b", A, B, P);
        $display("Expected Result: Product (P) = 10101 (21 in decimal)");
        $stop;             
    end
endmodule
