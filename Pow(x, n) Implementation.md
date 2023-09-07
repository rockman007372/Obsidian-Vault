---
tags: LeetCode, leetcode
topics: 
difficulty:
performance:
date: 2023-07-24 Monday
---

## Questions

Implement [pow(x, n)](http://www.cplusplus.com/reference/valarray/pow/), which calculates `x` raised to the power `n`.

## Solution

### Brute Force

```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n == 0:
            return 1
        if n > 0:
            return x * self.myPow(x, n - 1)
        if n < 0:
            return (1 / x) * self.myPow(x, n + 1)
```

Time and space: O(N)

### Recursion with optimized time

Notice that for even n:
$$x^{n} = (x ^ 2)^{\frac{n}{2}}$$
and for odd n:
$$x^{n} = x * (x ^ 2)^{\frac{n - 1}{2}}$$

This reduces the runtime to log(n), as we only iterate half of n in every iteration.

```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n == 0:
            return 1
        
        if n < 0:
            return 1 / self.myPow(x, -n)

        if n % 2 == 0:
            return self.myPow(x * x, n / 2)

        else:
            return x * self.myPow(x * x, n // 2)
```

### Iterative

```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n == 0:
            return 1

        if n < 0:
            x = 1 / x
            n = -1 * n

        res = 1
        while n != 0:
            
            if n % 2: # if odd
                res *= x
                n -= 1

            x = x * x
            n //= 2

        return res
```

---
Link: [[LeetCode]]
