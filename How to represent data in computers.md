---
tags: processed
course: CS2100
type: lecture
date: 2022-08-09 Tuesday
---
Links: [[CS2100]]
- - -

In C, all data are number. Same binary number can represent an `int` or `char`, dependent on variable type.

![[Pasted image 20220825154855.png]]

- N bits can represent $2^N$ values
	- Greatest number with N bits = $2^{N}- 1$ (*Inclusive of 0*)
- To represent M values or value M: $\lceil{log({M})}\rceil$
	- Why ceiling: if we take floor, 1 bit is missing, only M / 2 numbers can be represented

## Content 

1. [[Number System]]
2. [[Representing Sign and Magnitude in a Number System]]
3. [[Addition Operation on Complement Representation]]
4. [[Real Number Representation]]


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


