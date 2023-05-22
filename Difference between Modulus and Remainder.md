---
tags: math
aliases: 
sate: 2022-08-09 Tuesday
---
Links: [[Modulus Operator]]
- - -

Remainder is simply the remaining part after the arithmetic division between two integer number. 

Modulus is either:
- The sum of remainder and divisor when they are *oppositely signed* or
- The remaining part after the arithmetic division when remainder and divisor both *are of same sign.*

>[!note]
>In a % b:
> - Sign of remainder will be same as the divisible. (a)
> - Sign of modulus will be same as divisor. (b)

**Example of Remainder:**
```
10 % 3 = 1 [here divisible is 10 which is positively signed so the result will also be positively signed]

-10 % 3 = -1 [here divisible is -10 which is negatively signed so the result will also be negatively signed]

10 % -3 = 1 [here divisible is 10 which is positively signed so the result will also be positively signed]

-10 % -3 = -1 [here divisible is -10 which is negatively signed so the result will also be negatively signed]
```


**Example of Modulus:**
```
5 % 3 = 2 [here divisible is 5 which is positively signed so the remainder will also be positively signed and the divisor is also positively signed. As both remainder and divisor are of same sign the result will be same as remainder]

-5 % 3 = 1 [here divisible is -5 which is negatively signed so the remainder will also be negatively signed and the divisor is positively signed. As both remainder and divisor are of opposite sign the result will be sum of remainder and divisor -2 + 3 = 1]

5 % -3 = -1 [here divisible is 5 which is positively signed so the remainder will also be positively signed and the divisor is negatively signed. As both remainder and divisor are of opposite sign the result will be sum of remainder and divisor 2 + -3 = -1]

-5 % -3 = -2 [here divisible is -5 which is negatively signed so the remainder will also be negatively signed and the divisor is also negatively signed. As both remainder and divisor are of same sign the result will be same as remainder]
```
