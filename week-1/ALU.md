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
module ALU(
    input [3:0] a, b,
    input [2:0] op,
    output reg [3:0] result
);

always @* begin
    case (op)
        3'b000: result = a + b;
        3'b001: result = a - b;
        3'b010: result = a * b;
        3'b011: if (b != 0) result = a / b;
                else result = 4'b0000;
        3'b100: result = a | b;
        3'b101: result = a ^ b;
        default: result = 4'b0000;
    endcase
end

endmodule
```
## VERILOG TEST BENCH TO TEST ALU
```
module ALU_tb();

    reg [3:0] a, b;
    reg [2:0] op;
    wire [3:0] result;

    ALU uut (
        .a(a),
        .b(b),
        .op(op),
        .result(result)
    );

    initial begin
        $dumpfile("ALU.vcd");
        $dumpvars(1, ALU_tb);

        a = 4'b1011; b = 4'b1001; op = 3'b000; #10;
        a = 4'b1100; b = 4'b1001; op = 3'b101; #10;
        a = 4'b1001; b = 4'b1101; op = 3'b010; #10;
        a = 4'b1101; b = 4'b1111; op = 3'b100; #10;
        
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



