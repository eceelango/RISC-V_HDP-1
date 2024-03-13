# Design an 4-bit ALU in c code and verify it using gcc
## VIM Editor Installation

![Uploading Matrix Multiplication.png…]()

## ALU C CODE

```
#include <stdio.h>

int main() {
    int a, b, result;
    char operation[10];

    printf("Enter the value of a: ");
    scanf("%d", &a);
    printf("Enter the value of b: ");
    scanf("%d", &b);
    printf("Enter the required operation: ");
    scanf("%s", operation);

    if (strcmp(operation, "add") == 0) {
        result = a + b;
        printf("Value of %d + %d is %d\n", a, b, result);
    } else if (strcmp(operation, "sub") == 0) {
        result = a - b;
        printf("Value of %d %s %d is %d\n", a, operation, b, result);
    } else if (strcmp(operation, "mul") == 0) {
        result = a * b;
        printf("Value of %d %s %d is %d\n", a, operation, b, result);
    } else if (strcmp(operation, "div") == 0) {
        if (b == 0) {
            printf("Can't divide when b is zero\n");
        } else {
            result = a / b;
            printf("Value of %d %s %d is %d\n", a, operation, b, result);
        }
    } else {
        result = 0;
        printf("No operation is selected or invalid syntax\n");
    }

    return 0;
}
```
![Screenshot from 2024-03-13 18-32-57](https://github.com/Daniel4bit/RISC-V_HDP/assets/65249875/fe58d6ff-67e1-49c3-904e-acaba335221e)

## ALU VERILOG CODE
```
module alu(a,b,sel,result);
        input [31:0] a;
        input [31:0]b;
        input [1:0]sel;
        output reg [31:0] result;


        always@(*)
        begin
                case(sel)
                        2'b00 : result= a+b;
                        2'b01 :result=a-b;
                        2'b10 :result=a*b;
                        2'b11 :result=a/b;
                        default :result=32'b0;
                endcase
        end

endmodule
```
## VERILOG TEST BENCH TO TEST ALU
```
module alu_tb();

    // Inputs
    reg [31:0]a;
    reg [31:0]b;
    reg[1:0]sel;

    // Outputs
    wire [31:0] result;

    // Instantiate the Unit Under Test (UUT)
    alu  uut (
        .a(a),
        .b(b),
        .sel(sel),
        .result(result)
    );

    initial begin

            $dumpfile("alu.vcd");
             $dumpvars(1,alu_tb);

        // Apply inputs.
        a = 32'h0000000a;
        b = 32'h00000001;
        #50
        sel=0;
        #10
        sel=2'b10;
        #10
        sel=2'b11;
        #10
        sel=2'b01;
        #100
        $finish;
    end

endmodule
```


