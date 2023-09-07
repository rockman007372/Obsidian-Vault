---
tags: LeetCode, leetcode
topics: dp, math, memoize
difficulty:
performance:
date: 2023-06-29 Thursday
---

## Questions

You are given **two identical** eggs and you have access to a building with `n` floors labeled from `1` to `n`.

You know that there exists a floor `f` where `0 <= f <= n` such that any egg dropped at a floor **higher** than `f` will **break**, and any egg dropped **at or below** floor `f` will **not break**.

In each move, you may take an **unbroken** egg and drop it from any floor `x` (where `1 <= x <= n`). If the egg breaks, you can no longer use it. However, if the egg does not break, you may **reuse** it in future moves.

Return _the **minimum number of moves** that you need to determine **with certainty** what the value of_ `f` is.

## Solution

### Recursive + Memoize

Idea:
- Question does not care about how you solve the problem. You are not required to solve for f. **You are required to find the min no. moves to find f in the worst case scenario!**
- Try breaking the first egg at each floor:
	- If the egg breaks at floor i, you have to break the 2nd egg (i - 1) times more
	- If the egg does not break at floor i, you reduce the problem to (n - i) floor.

```python
class Solution:
    
    def twoEggDrop(self, n: int) -> int:
        memo = [None] * (n + 1)  
        def helper(n):
            nonlocal memo

            if n == 1:
                return 1

            if memo[n] :
                return memo[n]

            res = float('inf')
            for i in range(1, n):
                isBroken = i - 1
                isNotBroken = helper(n - i)
                res = min(res, max(isBroken, isNotBroken) + 1)

            memo[n] = res
            return res

        return helper(n)
```

One liner using Cache and Default argument:

```python
class Solution: 
	@cache 
	def twoEggDrop(self, n: int) -> int: 
		return min(
			(1 + max(i - 1, self.twoEggDrop(n - i)) for i in range (1, n)), 
			default = 1
		)
```


### Math

However, we can solve this problem using geometric sum.

Let x be the ideal minimum number of drops. Hence, we have to drop the egg at floor x initially, so that if the egg breaks, we only have to test x - 1 times with the 2nd egg. This makes up x steps.

If the egg does not break at floor x, we have to drop it at floor (2x - 1) for similar reason. 

In other word, the final floor to drop the first egg **so that x is the minimum drop in worst-case** must satisfy the inequality:
$$x + (x - 1) + (x - 2) + ... + 1 \geq n \iff \frac{x(x + 1)}{2} >= n$$

Hence we can solve for x:

```cpp
int twoEggDrop(int n) {
    int x = 1;
    while (x * (x + 1) / 2 < n)
        ++x;
    return x;    
}  
```

## Inversion and Generic Solution

With the help of the iterative solution above, we see that it's easier to solve an inverse problem: given `m` total drops, and `k` eggs, how high can we go?

So with one egg and `m` drops, we can only test `m` floors.

With two eggs and `m` drops:

1. We drop one egg to test one floor.
2. We add the number of floors we can test with `m - 1` drops and 2 eggs (the egg did not break).
3. And we add `m - 1` floors we can test with the last egg (the egg broke).

Thus, the formula is:

```
dp[m] = 1 + dp[m - 1] + m - 1;
```

... which is in-line with the observation we made for the iterative solution above!

This can be easily generalized for `k` eggs:

```
dp[m][k] = 1 + dp[m - 1][k] + dp[m - 1][k - 1];
```
---
Link: [[LeetCode]]
