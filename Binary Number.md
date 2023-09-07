2022-07-04 17:45
Tags: [[How to represent data in computers]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

## Binary to Decimal

Example:
$$110010 = 2^5 + 2^4 + 2^1$$

## Decimal to Binary

#### For Whole Number: Repeated Division of 2 

Algorithm:

```
int x;
binary number y;
while (x != 0) 
	y.append(x % 2)
	x = x / 2
return y.reverse();
```

![[Pasted image 20220809190206.png]]

**Quick tips:** 
- Most significant bits are *at the bottom* 
- To convert decimal number of binary number quickly:
	- Remember all the powers of 2 (1, 2, 4, 8, 16, 32, 64, 128...)
	- See how to fit all these powers into a number
	- EG: 18 → can fit 16, left with 2 → can fit 2 → $(18)_{10} = (10010)_{2}$
- *Number of bits* to store an integer x = $\lceil {log(x)} \rceil$
	- Why ceiling and not floor? If we floor, there will be one bit missing. The number of integers that can be represented is $\frac{x}{2}$

#### For Decimal Fractions: Repeated Multiplication of 2

![[Pasted image 20220809190321.png]]

- Tips:
	- Carry is the **whole number part** of the product.
	- We do multiplication on the **fractional part** of the product.
	- We stop when the **fractional part = 0**
	- Most significant bits are **on top!!**

## Bit Manipulation

See [[Adddition Using Bit Manipulation]]. 