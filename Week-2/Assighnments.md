# Assignment

## Using RISC-V GCC compiler (riscv64-unknown-elf-gcc) to compile a C source file (Counter.c) into an object file (Counter.o).
` riscv64-unknown-elf-gcc -march=rv64i -mabi=lp64 -ffreestanding -o ./Counter.o Counter.c`

` spike pk Counter.o` 


Let's break down the options used:

-march=rv64i: This specifies the RISC-V architecture variant to target. In this case, it's rv64i, indicating a 64-bit RISC-V ISA with the base integer instruction set (I).

-mabi=lp64: This specifies the ABI (Application Binary Interface) to use. lp64 stands for "long" and "pointer", indicating that int and long are 64 bits wide, as well as pointers.

-ffreestanding: This option tells the compiler that the program does not require a standard library, which is typical for embedded systems or kernels.

-o ./Counter.o: This specifies the output file name (Counter.o) for the compiled object file.

## Code for Counter.C
``` #include <stdio.h>
#include <time.h>

void delay(int n) {
    int us = n; // microseconds
    clock_t start_time = clock();
    while (clock() < start_time + (us * CLOCKS_PER_SEC / 1000000));
}

void display(int count) // Function to display the data on the four Led's
{
	printf("Count value is: %d\n", count);						
}

int main()
{
	int count = 0x00000000;
	while (1)
	{
		display(count);
		count++;
        if(count==16){
            count=0;
        }
		delay(500000);   // delay by 0.5 microseconds
	}
} ```c
