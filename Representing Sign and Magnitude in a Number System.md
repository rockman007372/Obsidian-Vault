Signed numbers representations include both positive number and negative numbers.

There are 4 common **representations** (*not a new number system*) for signed binary number:

1. [[Sign-and-Magnitude]]
2. [[1s-Complement]]
3. [[2s-Complement]]
4. [[Excess Representation]]

![[Pasted image 20220826104126.png]]

### Example Questions

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

How to negate a fractional number in 1s or 2s representation?

```
1s: 111000.101 → 000111.010 (Negate all the bits)
2s: 0101.01 → 1010.11 (Negate all the bits after LSB 1)
```

