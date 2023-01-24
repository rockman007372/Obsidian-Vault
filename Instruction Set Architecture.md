---
tags: 
aliases: 
---
Date:: 2022-09-07 Wednesday
Links: [[MIPS]]
- - -

### Instruction Set Architecture
- An abstraction on the **interface** between the hardware and software
- Allow many implementations of varying cost and performance to run identical softwares.

### RISC vs CISC
There are 2 major design philosophies for ISA:
- *Complex Instruction Set Computer* (CISC):
	- Example: x86-32
	- Single instruction performs complex operation
	- Smaller program size as memory was premium
	- Complex implementation, no hardware optimization
- **Reduced Instruction Set Computer** (RISC):
	- Example: MIPS, ARM
	- Keep the instruction set small and simple, easier to build and optimize
	- Burden on software to combine simpler operations to implement high-level language statement

### 5 Concepts in ISA Design
1. Data **Storage**: Where we get data?
2. **Memory Addressing** modes: How to access data from memory
3. **Operations** in the Instruction Set: Types of operations
4. Instruction **Formats**
5. **Encoding** the Instruction Set: Convert into binary bits

### Storage Architecture

For a processor, storage architecture concerns with:
- Where do we store the operands so the computation can be performed?
- Where to store computation results afterwards?
- How to specify the operands

4 common types of storage architectures:
1. **Stack**: Operands are implicitly on top of stack
2. **Accumulator**: 1 operand is implicitly in the accumulator (a special register)
3. General-purpose **register**: Explicit operands in register
   - Register-memory architecture: 1 operand in register, 1 in memory
   - Register-register architecture: both operands in registers (MIPS)
4. **Memory**-memory: Exlicit operands in memory

![[Pasted image 20221004014403.png]]

### Memory Addressing Mode
- Given k-bit address, address space is $2^k$
- Each memory transfer consist of one word of **n** bits
	- n = 0, 2, 4, 8, 16,...
	- In MIPS, one word = 32 bits = 4 bytes

**Edianness**: The relative ordering of bytes in a word, as stored in memory
- Big Edian: MSByte stored in the lowest address
- Small Edian: LSByte stored in the lowest address

![[Pasted image 20221004015602.png]]

How to address data: We can address data from register (add), from memory (lw/sw), from immediate values,...

### Instruction Format

3 types of instruction length:
- **Variable**-length ins: CISC
- **Fixed**-length ins: RISC
- Hybrid

Consists of operation and operands.

### Encoding 

Determines how instructions are represented in binary format for execution by the processor

Issues: Code size, speed & performance, design complexity

Things to consider inclue:
- Number of register: 32 register → 5 bits
- Number of addressing modes: more operations to encode
- Number of operands in an instruction: 

3 types of encoding:
![[Pasted image 20221004020609.png]]

#### Encoding in Fixed-length Instruction

Question: How to fit as many instructions as possible into the same limited number of bits?

Answer: **Expanding Opcode** scheme → The opcode has variable lengths for different instructions → No wasted bits and result in a larger instruction set.

Example:
>[!question]
> 16-bit fixed length instructions, with 2 types of instructions
> Type A: 2 operands, each operand is 5 bit long
> Type B: 1 operand of 5 bit length
> How to maximise/minimise number of instructions?

Under expanding opcode scheme:

![[Pasted image 20221004021305.png]]

**To maximise instruction sets, we maximise the instruction type with more bits!** Hence we allocate 1 instruction for type A and the remaining for type B.$$max = 1 + (2^{6} - 1)*2^{5} = 2017$$
To minimise ins set, we do the opposite: allocate 1 6-bit prefix for Type-B instruction and maximise A. $$min =(2^{6}- 1) +  2^{5} = 95$$
>[!Question]
> 3 instruction classes, A, B, C.
>A has 6 bit opcode
> B has 10 bit opcode
> C has 12 bit opcode
> What is the max/min number of instructions?

To find max instructions, subtract the instruction lost to class B and A from the total number of instructions then add the instructions gain:$$max = 2^{12}- 2^{2}+ 1 - 2^{6}+ 1=4030$$
To find min instructions, maximise the instruction with least bits, and repeat for instructions in decreasing length:$$min = (2^{6}- 1) + (2^{4}- 1) + (2^2) $$

>[!question]
>Design an expanding opcode for the following to be encoded in a 36-bit instruction format. Given an address takes up 15 bits and a register number 3 bits:
Type A: 7 instructions with two addresses and one register number.
Type B: 500 instructions with one address and one register number.
Type C: 50 instructions with no address or register.

We will start with the **most restrictive case!** In this case, we give the first 3 bits to the first 7 instruction.

![[Pasted image 20221004022323.png]]

Then we allocate the remaining free bits to other instructions.

![[Pasted image 20221004022403.png]]
