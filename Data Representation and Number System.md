---
tags: processed
course: CS2100
type: lecture
---
Date:: 2022-08-09 Tuesday
Links: [[CS2100]]
- - -

## Recitation Questions

##### Q1: How is 0.1 stored in C

```
Using what you know about number systems and C, show why this while loop may never end:  
  
float x = 0.0;  
while (x != 0.1)  
	x += 0.1;
```

0.1 is represented in IEEE754 format as:
$$0.1 = (0.000110...)_{2} = 1.10011... * (2^{-4})$$

```csharp
s eeeeeeee mmmmmmmmmmmmmmmmmmmmmmm    1/n
0 01111011 10011001100110011001101
           |  ||  ||  ||  ||  || +- 8388608
           |  ||  ||  ||  ||  |+--- 2097152
           |  ||  ||  ||  ||  +---- 1048576
           |  ||  ||  ||  |+-------  131072
           |  ||  ||  ||  +--------   65536
           |  ||  ||  |+-----------    8192
           |  ||  ||  +------------    4096
           |  ||  |+---------------     512
           |  ||  +----------------     256
           |  |+-------------------      32
           |  +--------------------      16
           +-----------------------       2
```

The sign is positive, that's pretty easy.

The exponent is `64+32+16+8+2+1 = 123 -> bias = 123 - 127 = -4`, so the multiplier is `2^(-4)` or `1/16`.

The mantissa is chunky. It consists of `1` (the implicit base) plus (for all those bits with each being worth `1/(2n)` as `n` starts at `1` and increases to the right), `{1/2, 1/16, 1/32, 1/256, 1/512, 1/4096, 1/8192, 1/65536, 1/131072, 1/1048576, 1/2097152, 1/8388608}`.

When you add all these up, you get `1.60000002384185791015625`.

When you multiply that by the multiplier, you get `0.100000001490116119384765625`, which is why they say you cannot represent `0.1` exactly in C.

##### Q2: Bit Shifting?

```C
char num = 0x11; // hex (base 16) = 16 + 1 = 17
num = 00010001; // binary, 17
num << 1 // = 00100010 = 34 (equivalent of times 2)
num >> 1 // = 0000100 = 8 (equivalent of divide by 2)
```

##### Q3: 2s Complement

> Find $(01001010)_2$ in 8-bit 2's complement

Ans: 01001010
- 2's complement is a **representation**, not an operation
- You only perform bit switching when converting from +ve to -ve and vice versa

##### Q4: 2s Complement

> Convert $(11010010)_{2s}$ to decimal

- Method 1: Apply formula$$x = -2^7 + 2^6 + 2^4 + 2^1 = -46$$
- Method 2: flip bits then add 1$$11010010 = 00101101 + 1 = 00101110 = 46$$ Since its negative, ans = -46

- Method 3: flip all the bits before the first 1, convert to decimal  then add negative sign$$11010010 = -(00101110) = -(46)$$

**Extra:** Find complement of 00101110 → 11010001 + 1 → 11010010

>[!important]
> Conclusion: Converting 2s complements back and forth are the same! **Invert everything then add 1** 

##### Q5: Complent Addition

> Find $00110011_{2s}$ + $00101010_{2s}$ in 8-bit 2s complement

```
00110011
00101010
--------
01011101

Same sign -> No overflow
```

##### Q6: Excess Representation

> Given an 8-bit number in excess-100 representation, how many negative values are there?

Ans: 100 LOL

Excess-100 means to get the number we want in binary, we add 100 to that number then convert to binary `100 + x -> binary`

x + 100 = 0 → smallest x = -100

##### Q7: IEEE-754 format

> Find 12.562 in IEEE-754 format, representing ur ans in 8 hexadecimal digits

![[Data Representation and Number System 2022-08-19 00.14.07.excalidraw]]


## 1. Number System
Basic datatypes in C:
- char (1 byte - 8 bits)
- int (4 bytes - 32 bits)
- float (4 bytes - 32 bits - IEEE754 Representation)
- double (8 bytes)
  
Same binary number can represent an `int` or `char`, dependent on variable type.

![[Pasted image 20220825154855.png]]

- N bits can represent $2^N$ values
	- Greatest number with N bits = $2^{N}- 1$ (*Inclusive of 0*)
- To represent M values or value M: $\lceil{log({M})}\rceil$
	- Why ceiling: if we take floor, 1 bit is missing, only M / 2 numbers can be represented

### Decimal Number
![[Pasted image 20220817195927.png]]

### Other Number Systems
1. [[Binary Number]]
2. Octal (Base 8)
	- {0, ... 7} digits
	- In C: `032` = $(32)_8$ = $3 * 8^{1} + 2$ = 26
3. Hexadecimal (Base 16)
	- {0..., 9, A, B, C, D, E, F} digits (to 15)
	- In C: `0x32` = $(32)_16$ = $3 * 16^{1} + 2$ = 50
4. Base/Radix R

### Base-R to Decimal Conversion
Same as above formula, just replace 10 with R → The factor is R

### Decimal to R-Conversion
- **Whole Number:** Repeated division by R
	- The remainders are the digits from left to right.
	- Most significant digit is the *last remainder*.
- **Fractional Number:** Repeated multiplication by R
	- Repeated until *fractional part of product is 0.*
	- Most significant digit in the beginning
- See [[Binary Number]] for more conversion info.

#### Conversion between different bases
- Just **change to Decimal first**, then convert
- **Shortcut:**
	- Binary to Octal: Partition in group of **3** → Why: 3 bits can represent max to 7 
		- Octal to Binary: Reverse
	- Binary to Hex: Partition in group of **4**
		- Hex to Binary: Reverse

![[Pasted image 20220817201330.png]]


## 2. Sign and Magnitude

Signed numbers representations include both positive number and negative numbers.

There are 3 common **representations** (*not a new number system*) for signed binary number:
1. Sign-and-Magnitude
2. 1s Complement
3. 2s Complement

### Sign-and-Magnitude
- 1 bit sign and 7 bit magnitude

![[Pasted image 20220825160155.png]]

- Largest value: $2 ^ 7 - 1$ = +127
- Smallest value: $-(2 ^ 7 - 1)$ = -127
- 2 zeros representation: `0000000` (+0) and `1000000` (-0)
- Range: -127 to 127 (256 numbers)
- For an n bit size-and-magnitude, range = $-2^{n - 1} +1$ to $2 ^ {n - 1}-1$
- To negate, invert the **sign** bit

### 1s-Complement

>[!Definition]
> Given number x which can be expressed as an n-bit *binary number*, its negated value in 1s Complement representation is:
$$-x = 2^{n}- 1- x$$

Negated value of 12 in *8-bit 1s' complement* representation:
$$-12 = -(00001100) = 2 ^ 8 - 1 - 12 = (243)_{10} = 11110011 $$

- Largest = +127
- Smallest = -127
- 2 Zeros: -0 and +0
- **MSB** represents the sign
- Technique to negate value: **invert all the bits**.

To convert a **1s-complement representation → decimal**:
- For positive number: **Normal** Binary to Decimal conversion
	- 14 = $(00001110)_2$ = $(00001110)_{1s}$ 
- For negative number: 
	- Bit-inversion: $-14 = -(00001110) = 11110001$
	- Formula: $11110001 = - 2^7 + (64 + 32 + 16 + 1) + 1 =  -14$
	- **Shortcut:** $11110001 = -(00001110) = -14$

### 2s-Complement

>[!Definition]
> Given number x which can be expressed as an n bit *binary number*, its negated value in 2s Complement representation is:
$$-x = 2^{n}- x$$

Example: 

Negated value of 12 in 2s complement rep:
$$-12 = -(00001100) = 2 ^ 8 - 12 = (244)_{10} = (11110010)_{2s}$$

- Largest = +127
- Smallest = -128
- 1 Zero: 00000000
- **MSB** represents the sign
- Technique to negate value: 
	- Invert all the bits, then add 1
	- Shortcut: **Invert all the bits after the least significant 1**.

To convert a 2s -Complement Representation to Decimal:
- For positive number: **Normal** Binary to Decimal conversion
	- 14 = $(00001110)_2$ = $(00001110)_{2s}$ 
- For negative number: 
	- -14 = $-(00001110)_2$ = 11110010
	- 11110010 = $- 2^7 + (64 + 32 + 16 + 2)$ =  -14
	- **Shortcut:** 11110010 = -(00001110) = -14 → **We can negate this negative values using either of the 2 techniques above, then add a negative**

![[Pasted image 20220826104126.png]]

Past Year Question:

```C
int i, n = 2147483640;
for (i = 1; i <= 10; i++) {
	n = n + 1;
}

printf("n = %d\n", n);

// What is the output of this code on Sunfire?

/*

Sunfire uses 2s-complement representation. Int type has 4 bytes (32 bits)

Max int represented = 2 ^ 31 - 1 = 2147483647

Hence if we go into the loop:

itertation 0: 2147483640
...
iteration 7: 2147483647 = (0111111111111111.....)_2 
interation 8: (100000000...) = -2147483648
iteration 9: 10000...1 = -2147483647
interation 10: 10000...10 = -2147483646 → answer
*/
```

### Complement on Fractions

```
1s: 111000.101 → 000111.010 (Negate all the bits)
2s: 0101.01 → 1010.11 (Negate all the bits after 1)
```


## 3. Complement Addition

### Overflow
Signed numbers are of fixed range, hence overflow can occur if result of additon/subtraction exceeds this range.

Oveflow can easily be detected:
- positive + positive → negative
- negative + negative → positive

Example: 4-bit 2s-complement system
- Range: -8 to +7
- 5 + 6 = 0101 + 0110 = 1011 = -5?
- -7 + (-3) = 1001 + 1101 = 0110 = 6?

### 2s Complement on Addition and Subtraction

Addtion:
1. Perform binary addition
2. **Ignore the carry out of the MSB**
3. Check for overflow (look at sign / check carry in != carry out)

Subtraction: 
1. Take 2s-complement of B
2. Addition

### 1s Complement on Addition and Subtraction

Addtion:
1. Perform binary addition
2. **Add the carry out of the MSB** to result (add 1 to result)
3. Check for overflow (look at sign difference)

Subtraction: 
1. Take 1s-complement of B
2. Addition
 
 ![[Pasted image 20220826110507.png]]

### Excess Representation
- Another schemes to represent signed numbers
- Distribute positive and negative values **evenly** accross the range of values by a translation.
- Example: excess-4 representation of 3-bit numbers
	- 4 negative numbers
	- 3 bits → $2 ^ 3$ = 8 numbers represented → We take 4 negative and 4 non-negative
	- By convention: the number of excess of an n bit number = $2^{n - 1}$ or $2^{n - 1} - 1$

![[Pasted image 20220826110831.png]]

## 4. Real Number Representation

Due to finite number of bits → Real numbers are stored as *approximate values* (eg: 0.1 cannot be stored exact in C). Below are some representations:

##### Fixed-Point Representation

Number of bits for whole number and fractional number are fixed.

![[Pasted image 20220826111352.png]]

Example: Using 2s-Complement system
$$011010.11 = 26.75$$$$111110.11 = -(000001.01) = -1.25$$

With 2 bits for decimal points, you can represent 4 values → Each bit equals 0.25 → **Extremely low precision**

##### IEEE 754 Floating-Point Representation

![[Pasted image 20220826111726.png]]

- Base (radix) is 2.
- 2 formats:
	- **Single-Precision** (32 bits): 1-bit sign, 8-bit exponent with excess 127, 23-bit matissa
	- Double-Precision (64 bits)
- Matissa is **normalized** with an implicit leading bit 1 → Save 1 bit → double the representation!

Example: To store number -6.5
 $$-6.5 = -(110.1) = -(1.101 * 2^2)$$
-  Store negative sign (1)
- Store 2 in exponential with excess 127 → Exponent = 2 + 127 = 129
- Only 101 is stored in mantissa

![[Pasted image 20220826112658.png]]

We can convert binary rep to **hexadecimal** by dividing into **chunks of 4 bits**: $(C0D00000)_{16}$
