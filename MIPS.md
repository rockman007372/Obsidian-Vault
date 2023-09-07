---
tags: processed
course: CS2100
type: lecture
date: 2022-09-01 Thursday
---

Higher-lever language written by programmer → Translated by Compiler into machine language → Translated by Assembler into machine code

## Components in Computer

- 2 major components:
	- Processor: perform computations, containing **registers** which are temporary memory
	- Memory: Storage of code and data
	- Connected by a bus (wire/circuits)

- Load-store model: Data are transferred into memory and **stored in register** to save time during computation, and **loaded back into memory** as computed results.

## General Purpose Registers

- Purpose: Faster computation in processor
- Limited in numbers - typical architecture has 16 to **32 registers**
- Compiler associates variables with registers
- Registers have no **data type** → Weakly typed → Assembly relies on instructions to interpret types
- `$s0 to $s7`: Program variables 
- `$t0 to $t7`: Temporary variables

![[Pasted image 20220904101434.png]]

## MIPS topics

1. [[MIPS Basic Instructions]]
2. [[Memory Organization In MIPS]]
3. [[Control Flow In MIPS]]
4. [[Instruction Format in MIPS]]
5. [[Instruction Set Architecture]]

## Summary
##### Arthimatic and Logical Operations
![[Pasted image 20220904005337.png]]


## Questions/Cues

###### Q1. Instruction in Memory
- An instruction is fetched from 0x400028. Where will the next instruction be?
	- Instructions are stored in Memory. Each instruction takes 4 bytes to store. 
	- Hence 0x400028 + 4 = 0x40002C != 0x400032 (WE ARE COUNTING IN HEX!)

###### Q2. ORI
- What does `ori t0, t0, 0x0000` do?
	- Keep all the bits in t0
	- No sign-extension → Extended with 0s
	- Any bit `or` 0 = the same bit
	  
###### Q3. Branch
- `beq s0, s1, 4` or `beq s0, s1, exit` can specify the full 32 bit address to branch to?
	- False
	- 4 / `exit` is a **16-bit offset**, not a full 32 bit address
	- Using the offset, we can branch to any **address** within the range of $-2^{15}$ to $(2^{15} - 1)$ from the current instruction addresss
	- Hence we cannot branch to any address in memory!

![[MIPS 2022-09-04 10.34.42.excalidraw]]

###### Q4. Memory Instruction: sw and lw
>`sw t1, 160($0)` What does this instruction do?

Copy data from register t1 to address 160

`$0 ` stores 32-bits 0s (0x00000000) → Compiler interprets this value as an *address* due to the instruction → Plus 160 bytes in decimal!

Look at the format of the number! eg. `0x`

$0 + 160 must be a **multiple of 4**

###### Q5. XOR
>`xor s0, s0, s0` what effect does this do?

It has the same effect as `and s0, s0, 0x0000` → Clear 32 bits to 0s




###### Q6. What is the size of the memory needed to store a program?
An instruction takes up 4 bytes (32 bits) in memory → 4 * Number of instructions



