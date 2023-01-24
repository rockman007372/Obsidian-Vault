---
tags: MIPS
aliases: 
---
Date:: 2022-09-07 Wednesday
Links: [[MIPS]]
- - -

## Control Instructions
### Conditional branch: beq and bne

`beq $r1, $r2, L1` → Go to statement labeled `L1` if value in `r1` equals `r2`

`bne $r1, $r2, L1` → Go to statement labeled `L1` if value in `r1` is NOT equal to `r2`

![[Pasted image 20220907232050.png]]

We can do **condition inversion** to reduce code lengths:

```C
if (i == j)
	f = g + h;
```
```MIPS
// Can be converted to MIPS as
	beq $s3, $s4, L1
	j   Exit
L1: add $s0, $s1, $s2
Exit:
```
```MIPS
// Or by using condition inversion
	bne $s3, $s4, Exit
    add $s0, $s1, $s2
Exit:
```

### Unconditional branch: j
![[Pasted image 20220907232140.png]]

### Inequalities: slt

```MIPS
slt $t0, $s1, $s2 # set on less than

bne $t0, $zero, L # if s1 is less than s2, branch to L
                  # equivalent to "beq $t0, ones, L".
                  # But we dont have to load 1s into a register 

```

`slt $t0, $s1, $s2` is equivalent to `s0 = s1 < s2 ? 1 : 0`

## IF statement

```C
if (i == j)
    f = g + h;
else
    f = g - h;
```

```MIPS
	   bne $s3, $s4, Else
       add $s0, $s1, $s2
       j   Exit
 Else: sub $s0, $s1, $s2
 Exit:
```

## Loops
### While Loop
```C
while (j != k) 
	j = j + 1;
```
```
Loop: beq  $s4, $s5, Exit
	  addi $s4, $s4, 1 
      j    Loop
Exit:
```

### For Loop
```C
for (int i = 0; i < 10, i++) {
	a = a + 5;
}
```

```
// Mapping
i → s0
a → s2
```

```
addi s0, $zero, 0
addi s1, $zero, 10
Loop: beq s0, s1, Exit
	  addi s2, s2, 5
	  addi s0, s0, 1
	  j    Loop
Exit:
```

## Array & Loop

Process:
1. Initialize:
	1. Result
	2. Loop counter
	3. Array Pointer
2. Compare and branch to exit if condition is met, else:
	1. Calculate address
	2. Load data
	3. Perform tasks
	4. Update loop counters and pointers
	5. Loop to 2

```C
int A[] = {...}

result = 0;
i = 0;
while ( i < 40 ) {  
	if ( A[i] == 0 )  
	  result++;  
	i++;
}
```

We store **address** in the register as a **pointer**, and increment pointer by 4 to reach the next element in the array:

```MIPS
-------------------------
Address of A[] → $t0

Result → $t8

&A[i] → $t1

-------------------------

addi  $t8, $zero, 0

      addi $t1, $t0, 0

      addi $t2, $t0, 160  # 40 * 4, addr of the first element after A[] 

loop: beq  $t1, $t2, end

      lw   $t3, 0($t1)

      bne  $t3, $zero, skip

      addi $t8, $t8, 1 

skip: addi $t1, $t1, 4   # Increment address pointer

      j loop

end:
```

