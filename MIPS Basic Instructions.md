---
tags: MIPS, Assembly Language
aliases: 
date: 2022-09-07 Wednesday
---
Links: [[MIPS]], [[Adddition Using Bit Manipulation]]
- - -
## Arithmetic Operation

```Python
add $s0, $s1, $s2 

addi $s0, $s1, 100 # Add immediate

sub $s0, $s1, $s2 

addi $s0, $s1, -100 # Substract a constant

addi $s0, $s1, $zero # Assignment
```

Important concepts:
- MIPS operations are mainly register-to-register
- For longer operations (s = a + b - c), do step-by-step: `a = a + b` then `s = a - c `
- `Addi`: add immediates (constant) → **The constant is a 16-bit 2s-complement number** → Ranges from $-2^{15}$ to $2^{15}-1$
- There is no `subi` → Use `addi` with a negative constant!
- To do assignmnent, use `addi` and `zero` → `addi $s0, $s1, $zero`

## Logical Operators

![[Pasted image 20220904002037.png]]

### Shifting

```
sll t2, s0, 4 # shift left logical: <<4 = multiply s0 by 2^4 = 16
srl t2, s0, 2 # shift right logical: >>2 = divide s0 by 2^2 = 4
```

- Can shift a maximum of **31 bits** = $2^5 - 1$ → Shift anymore bits and we get 0, and MIPS does not allow shifting beyond 31 bits.
- We use `sll` and `srl` to do multiplication/division by multiple of 2.

### Bitwise AND

```Python
x & 1 = x
x & 0 = 0
```

Used for **masking**: Only keeping the interested bits, the rest flipped to 0
- Place 0s in the position to ignore → Bits turned to 0s
- Place 1 in the interested position → Bits will *remain the same as original*

![[Pasted image 20220904002734.png]]

Example:
```
andi t1, t1, 0xFFF # We mask the last 12 bits of t1
```

![[Pasted image 20220904002936.png]]

**Important:**
- `andi` only takes in a raw 16 bit as immediate → The remaining upper 16 bits are extended with 0s (not sign extended)
- To do bitwise operations on 32-bit immediate, we have to load the immediate into a separate register and perform bitwise `and`

### Bitwise OR

```python
x or 0 = x
x or 1 = 1
```

Purposes:
1. Used to **force certain bits to 1**
2. Assignment: `or 0` to keep bits **unchanged**.

Example:

```
ori t0, t1, 0xFFF # Force last 12 bits to 1
```

![[Pasted image 20220904003143.png]]

```
ori t0, t1, zero # t0 = t1
```

**Important:**
- `ori` immediate is **NOT sign-extended** 

### Bitwise NOR

`nor` is equivalent of `~or`:

![[Pasted image 20220904003636.png]]

We can perform `not` operations by `nor` with `0s`

```
nor $t0, $t0, $zero # nor with 0 flip the bits
```

### Bitwise XOR

`xor` is equivalent of **NOT EQUAL**

![[Pasted image 20220904003942.png]]

We can perform `not` operation by `xor` with `1s`

```
lui $t1, 0xFFFF
ori $t1, $t1, OxFFFF
xor $t0, $t0, $t1      # Flip all the bits in $t0
```

We CANNOT perform `not` using  `xori t0, t0, 0xFFFF`  → This will only load the lower 16 bits to 1s. *The upper 16 bits are 0s*

### How to load large 32-bit constant into registers
- Immediate (constants) are only 16-bit long! It may or may not be sign-extended → *dependent on the instructions*
- 2 steps to load large constant: `lui` + `ori`

```java
1. Use lui (Load Upper Limit) to set the upper 16-bit:

lui $t0, 0xAAAA // 1010 1010 1010 1010 

t0 = 1010 1010 1010 1010 | 0000 0000 0000 0000

2. Use ori to set the lower-order bits:

ori $t0, $t0, OxF0F0 // 1111 0000 1111 0000

t0        = 1010 1010 1010 1010 0000 0000 0000 0000 
immediate = 0000 0000 0000 0000 1111 0000 1111 0000
---------------------------------------------------
t0        = 1010 1010 1010 1010 1111 0000 1111 0000
```


## Summary

![[Pasted image 20220904005337.png]]
