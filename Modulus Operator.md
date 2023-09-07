---
tags: computerScience, math
aliases: 
---
### For positive numbers
(This explanation is only for positive numbers since it depends on the language otherwise)

**Definition**

The _Modulus_ is the remainder of the euclidean division of one number by another. `%` is called the _modulo operation_.

For instance, `9` divided by `4` equals `2` but it remains `1`. Here, `9 / 4 = 2` and `9 % 4 = 1`.

![Euclidean Division](https://i.stack.imgur.com/03s5V.png)

In your example: 5 divided by 7 gives 0 but it remains 5 (`5 % 7 == 5`).

**Calculation**

The modulo operation can be calculated using this equation:

```
a % b = a - floor(a / b) * b
```

-   `floor(a / b)` represents the number of times you can divide `a` by `b`
-   `floor(a / b) * b` is the amount that was successfully shared entirely
-   The total (`a`) minus what was shared equals the remainder of the division

Applied to the last example, this gives:

```
5 % 7 = 5 - floor(5 / 7) * 7 = 5
```

