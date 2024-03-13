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
## iVerilog Installation
![Screenshot from 2024-03-13 18-39-13](https://github.com/Daniel4bit/RISC-V_HDP/assets/65249875/665a66ad-f486-42b1-b5ca-e0d65766a615)
Below are the instructions for completing the assignment:
Installing Iverilog on Ubuntu:

Icarus Verilog (Iverilog) is an open-source simulator that supports the Verilog hardware description language (HDL) and is commonly used in small-scale projects for digital circuit design and verification.

    Go to the official Icarus Verilog GitHub repository. Select the V12-branch and download https://github.com/steveicarus/iverilog/tree/v12-branch?ref=circuitcove.com

    Open a terminal window and navigate to the directory where the zip or tarball was downloaded. Then, unpack the tarball or unzip using the following command:

    unzip iverilog-12-branch.zip

    cd iverilog-12-branch

    Run the autoconf script to generate the configure file using the following command:

    sh ./autoconf.sh

    Run the configure script using the following command:

    ./configure

    Build Icarus Verilog using the make command:

    make

    Install Icarus Verilog using the following command:

    sudo make install

## Installing Gtkwave on Ubuntu:

    gtkwave is a viewer for VCD (Value Change Dump) files which are usually created by digital circuit simulators.

    sudo apt-get update

    sudo apt-get -y install gtkwave

## Verifying the Verilog Code using iverilog and gtkwave:
Install iverilog and gtkwave on your Ubuntu system (instructions provided). Compile the Verilog code using iverilog. Simulate the compiled Verilog code using vvp. Use gtkwave to visualize the simulation waveform and verify the functionality of the Verilog ALU.


![Screenshot from 2024-03-13 21-41-58](https://github.com/Daniel4bit/RISC-V_HDP/assets/65249875/3cf24a9c-254e-489f-b1c0-21e5644ef7ca)

`Daniel:~/Desktop/HDL$ sudo apt install libcanberra-gtk-module`
![2](https://github.com/Daniel4bit/RISC-V_HDP/assets/65249875/075c20c5-c651-4393-96b2-2c03871a72c6)

![Screenshot from 2024-03-13 21-48-23](https://github.com/Daniel4bit/RISC-V_HDP/assets/65249875/8e3ec3c1-134d-4a48-9eac-b7b844d276ba)

`Click ALU_tb in the GTKWAVE window, Types and signals will appear, from there drag each signal to 'signals' window to visualize the graph.



