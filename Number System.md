## Common Number Systems

1. [[Binary Number]] (Base 2)
2. Octal (Base 8)
	- {0, ... 7} digits
	- In C: `032` = $(32)_8$ = $3 * 8^{1} + 2$ = 26
3. Decimal (Base 10) 
4. Hexadecimal (Base 16)
	- {0..., 9, A, B, C, D, E, F} digits (to 15)
	- In C: `0x32` = $(32)_16$ = $3 * 16^{1} + 2$ = 50
5. Base/Radix R

## Base-R to Decimal Conversion

![[Pasted image 20220817195927.png]]

Same as above formula, just replace 10 with R → The factor is R

$$
\begin{align*}
(a_{n}a_{n-1}...a_{0},f_{1}f_{2}...f_{m})_{R} = \\ a_{n}*R^{n}+ a_{n-1}*R^{n-1} + ... + a_{0} \\ + f_{1}* R^{-1} + f_{2}*R^{-2} + ... f_{m} * R^{-m}
\end{align*}
$$

## Decimal to R-Conversion

- **Whole Number:** Repeated division by R
	- The remainders are the digits from left to right.
	- Most significant digit is the *last remainder*.
- **Fractional Number:** Repeated multiplication by R
	- Repeated until *fractional part of product is 0.*
	- Most significant digit in the beginning

## Conversion between different bases

- Just **change to Decimal first**, then convert
- **Shortcut:**
	- Binary to Octal: Partition in group of **3** → Why: 3 bits can represent max to 7 
		- Octal to Binary: Reverse
	- Binary to Hex: Partition in group of **4**
		- Hex to Binary: Reverse

![[Pasted image 20220817201330.png]]