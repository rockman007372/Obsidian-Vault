Assuming we have 8 bits to work with. We can represent a signed number using:

- 1 bit sign 
- 7 bit magnitude

![[Pasted image 20220825160155.png]]

- Largest value: $2 ^ 7 - 1$ = +127
- Smallest value: $-(2 ^ 7 - 1)$ = -127
- 2 zeros representation: `0000000` (+0) and `1000000` (-0)
- Range: -127 to 127 (256 numbers)
- For an n bit size-and-magnitude, range = $(-2^{n - 1} +1)$ to $(2 ^ {n - 1}-1)$
- To negate, invert the **sign** bit