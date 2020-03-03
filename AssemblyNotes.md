# Jeremy's Assembly notes

## Syntax

* Comments: One line starting with #
* Statements: One line does one thing
    * Example: movq     %rdx, %rbx | That moves rdx register to rbx
* ".globl   multstore" notifies linker of location multstore
* at some point (one or two lines down normally), "multstore:" will start its own line
* Variables: Registers and memory, sometimes named locations
* Assignments: Instructions that put bits in registers/memory
* Functions: Code locations that are labled and global
* Conditionals/Iteration: Assembly instructions that jump to code locations
* Aggregate Data: NONE, need to use stack/multiple registers
* Library System: link to other code

### Register Overview

* Syntax states they should be named with "%" at the start
* Instruction and register names note whether 16 bit (not used), 32 bit, or 64 bit
* Register names and function endings based off of sizes:

| **Bits**  | **Suffix**    | **Naming Convention**     |
| :-------: | :-----------: | :-----------------------: |
| 8         | -b            | %al, %bl, %cl, etc.       |
| 16        | -w            | %ax, %bx, %cx, etc.       |
| 32        | -l            | %eax, %ebx, %ecx, etc.    |
| 64        | -q            | %rax, %rbx, %rcx, etc.    |

### Register Functions

* mov: Moves Memory
* vmov: Moves Memory (Floating-Points)
* push, pop: Stack Functions
* Arithmetic Functions
    * add, sub: Basic Addition and Subtraction
    * mul, div: Unsigned Multiplication/Division
    * imul, idiv: Signed Multiplication/Division
    * vadd,vsub,vmul,vdiv: Same As Above But For Floating-Points
    * inc, dec: +1 Operations
    * neg: Negate
    * not: Complement
* Bitwise
    * and,or,xor,not: Bitwise logicals
    * sal, shl: Left Shifts (Identical)
    * sar: Right Shift (Signed)
    * shr: Right Shift (Unsigned)
* Conditionals:
    * cmp, test: Compare and Test
    * jmp: Unconditional Jump
    * je,jne: Jump If (Not) Equal
    * jl,jg: Jump If Less Than/Greater Than
* Conditional Movement
    * cmove, cmovne: Move If (Not) Equal
    * cmovl, cmovg: Move If Less Than/Greater Than
* Call/Return call,ret
* syscall: Place system call number in %rax, and then args in normal order, then then syscall
* lea: Load Address Into (Address-Of) - Ex: leaq 8(%rdx),%rax # rax = rdx+1 = \#1032

### Use of Each Variable

* Return Value: %rax, %eax, %ax, %al
* Arg 1: %rdi, %edi, %di, %dil
* Arg 2: %rsi, %esi, %si, %sil
* Arg 3: %rdx, %edx, %dx, %dl
* Arg 4: %rcx, %ecx, %cx, %cl
* Arg 5: %r8, %r8d, %r8w, %r8b
* Arg 6: %r9, %r9d, %r8w, %r8b
* Stack Ptr: %rsp, %esp, %sp, %spl
* (Might Not Exist) Base Ptr: %rbp, %ebp, %bp, %bpl

### Operands and Addressing Modes

| **Style**         | **Mode**      | **C-equivalent**      |
| :---------------: | :-----------: | :-------------------: |
| $21/$0xD2         | Immediate     | 21/0xD2 (210)         |
| %rax              | Register      | rax                   |
| (%rax)            | Indirect      | *rax                  |
| 8(%rax)           | Displaced     | *(rax+2)              |
| (%rax, %rbx)      | Indexed       | *(rax+rbx)            |
| (%rax, %rbx, 4)   | Scaled index  | *rax[rbx] (size of 4) |
| 1024              | Absolute      | ... (Address #1024)   |
