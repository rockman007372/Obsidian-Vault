Assuming we have 8 bits to represent a signed integer. We can represent it in 1s-complement representation using this formula:

>[!Formula]
> Given number x which can be expressed as an *n-bit binary number*, its negated value in 1s-complement representation is:
$$-x = 2^{n}- 1- x$$

Negated value of 12 in *8-bit 1s-complement* representation:
$$-12 = -(00001100) = 2 ^ 8 - 1 - 12 = (243)_{10} = 11110011 $$

- Largest value = +127
- Smallest value = -127
- 2 Zeros: -0 and +0
- **MSB** represents the sign
- Technique to negate value: **invert all the bits**.

#### Converting Decimal to 1s-complement representation 

For positive number: Perform Binary-to-Decimal conversion as per usual.
	$$14 = (00001110)_2 = (00001110)_{1s}$$ 
For negative number: Bit inversion

$$-14 = -(00001110) = 11110001$$


#### Converting 1s-complement to Decimal

Positive number: as per usual.
Negative number:
- Using formula: $$11110001 = - 2^7 + (64 + 32 + 16 + 1) + 1 =  -14$$
- Using bit-inversion **shortcut:** $$11110001 = -(00001110) = -14$$