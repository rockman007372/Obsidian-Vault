---
tags: MIPS
aliases: 
date: 2022-09-07 Wednesday
---
## Memory
- Main memory = 1D array of bytes.
- Each byte has an **address** (index) 
	- Given a k bit address, the address space has size $2^k$
- Each address location contains 1 byte = 8 bits

![[Pasted image 20220904011353.png]]

## Word
- Usually contain $2^n$ bytes
- Common unit of transfer between processor and memory
- Coincide with register size, integer size and **instruction size** (4 bytes = 32 bits)
- **Word alignment:** Words are aligned if the **byte address** is a **mutiple** of the number of bytes in a word
![[Pasted image 20220904011709.png]]

## MIPS Memory Instructions
- 32 **registers**, each is 32-bit (4 bytes) long
- Each **word** contains 32 bits (4 bytes)
- Memory **addresses** are 32-bit long → Address size = $2^{32}$
- Number of memory words = $2^{30}$ = $\frac{2 ^ {32}}{2 ^ 2}$ 
	- MIPS uses Byte address (Each address holds 1 byte)
	- Consecutive words differ by 4 bytes (4 addressses)

![[Pasted image 20220904012222.png]]

### Load Word
![[Pasted image 20220904012340.png]]

### Store Word
![[Pasted image 20220904012426.png]]

### Load and Store Word in Arrays

![[MIPS 2022-09-04 01.27.00.excalidraw]]

### Other Memory Instruction

```python
lb $t1, 12($s3) # load the 12th byte away from address in s3 into register t1

sb $t1, 13($s3) # offset can be anything, no need to be multiple
```

Same working except only 1 byte is loaded/stored instead of 1 word (4 bytes) → Offset is no longer needed to be a mutiple of 4!

MIPS disallows loading/storing **unaligned words** using `lw` and `sw` → Can use `ulw` and `usw`

### Address vs Value

A register can hold any 32-bit number:
- It could be an *address* or a *signed data value*
- Interpreted according to the instructions

![[Pasted image 20220904013909.png]]

### Swapping elements

```C
swap(int v[], int k) {
	int temp;
	temp = v[k];
	v[k] = v[k + 1];
	v[k + 1] = temp;
}
```

```C
# Variable mappings
k → s5
v[0] → s4
temp → s15

# MIPS code
swap:
	sll s2, s5, 2     # s2 = s5 * 4
	add t0, s4, s2    # get address of v[k] = addrs of v[0] + s2

	lw s15, 0(t0)
	lw s16, 4(t0)
	
	sw s15, 4(t0)
	sw s16, 0(t0)
```