Assuming we have 8 bits to work with. We can represent a signed number using 2s-complement representation.

>[!Formula]
> Given number x which can be expressed as an *n-bit binary number*, its negated value in 2s Complement representation is:
$$-x = 2^{n}- x$$


Negated value of 12 in *8-bit 2s-complement* rep:
$$-12 = -(00001100) = 2 ^ 8 - 12 = (244)_{10} = (11110100)_{2s}$$

- Largest value = +127
- Smallest value = -128
- 1 Zero: 00000000
- **MSB** represents the sign
- Technique to negate value: 
	- Invert all the bits, then add 1
	- Shortcut: **Invert all the bits after the least significant 1**.


#### Converting Decimal to 2s-complement 

For positive number: normal conversion
$$14 = (00001110)_2 = (00001110)_{2s}$$
For negative number: Invert then add 1
$$-14 = -(00001110)_2 = 11110001 + 1 = 11110010$$

#### Converting 1s-complement to Decimal

Using formula: $$11110010 = - 2^7 + (64 + 32 + 16 + 2) =  -14$$
Using shortcut:
$$11110010 = -(00001110) = -14$$
→ **We can negate the value (11110010 to 00001110), then add a negative sign**