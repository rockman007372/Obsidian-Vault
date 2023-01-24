2022-07-04 18:07
Tags: [[Binary Number]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Addition Using Bit Manipulation

> Given 2 binary numbers, a and b, calculate its sum in binary form without using "+".

We will make use of 3 operators:

`^ XOR` → Simulate addition -  sum of two binaries without taking carry into account
1 ^ 1 = 0 ^ 0 = 0
1 ^ 0 = 0 ^ 1 = 1

`&` → Find postion of carry

`<<1` → Find the next position of carry

See also: [Bit manipulation operations](https://www.interviewcake.com/concept/java/bit-shift)

eg:
```Java
	1100 (12)
+
	1010 (10)
-----------------------------------------------------
sum-without-carry = 1100 xor 1010 = 0110
carry (where to apply carry) = 1100 & 1010 = 1000
carry-adjusted-to-left = 1000<<1 = 10000
-----------------------------------------------------
sum = 00110 xor 10000 = 10110
carry-adjusted = (00110 & 10000)<<1 = (00000)<<1 = 0
-----------------------------------------------------
Since carry = 0, we can stop.
Result = 10110 = 22
```


```Python
# a store result, b store carry
while (b != 0): 
	a = a ^ b         # hold current result
	b = (a & b)<<1    # hold the next carry shifted to the left
return a;             # if carry is 0, we just return result since a xor 0 = a
```