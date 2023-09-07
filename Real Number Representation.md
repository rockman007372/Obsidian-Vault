
Due to finite number of bits → Real numbers are stored as *approximate values* (eg: 0.1 cannot be stored exact in C). 2 ways to represent real numbers:
- Fixed-point Representation
- IEEE 754 Floating-Point Representation

## Fixed-Point Representation

Number of bits for whole number and fractional number are fixed.

![[Pasted image 20220826111352.png]]

Example: Using 2s-Complement system
$$011010.11 = 26.75$$$$111110.11 = -(000001.01) = -1.25$$

With 2 bits for decimal points, you can represent 4 values → Each bit equals 0.25 → **Extremely low precision**

## IEEE 754 Floating-Point Representation

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