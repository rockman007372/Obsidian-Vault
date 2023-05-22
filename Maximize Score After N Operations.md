---
tags: LeetCode, leetcode
topics: dp, memoization
difficulty: hard
performance: uncomplete
date: 2023-05-16 Tuesday
---

## Questions

You are given `nums`, an array of positive integers of size `2 * n`. You must perform `n` operations on this array.

In the `ith` operation **(1-indexed)**, you will:

-   Choose two elements, `x` and `y`.
-   Receive a score of `i * gcd(x, y)`.
-   Remove `x` and `y` from `nums`.

Return _the maximum score you can receive after performing_ `n` _operations._

The function `gcd(x, y)` is the greatest common divisor of `x` and `y`.

**Example 1:**

**Input:** nums = [1,2]
**Output:** 1
**Explanation:** The optimal choice of operations is:
(1 * gcd(1, 2)) = 1

**Example 2:**

**Input:** nums = [3,4,6,8]
**Output:** 11
**Explanation:** The optimal choice of operations is:
(1 * gcd(3, 6)) + (2 * gcd(4, 8)) = 3 + 8 = 11

**Example 3:**

**Input:** nums = [1,2,3,4,5,6]
**Output:** 14
**Explanation:** The optimal choice of operations is:
(1 * gcd(1, 5)) + (2 * gcd(2, 4)) + (3 * gcd(3, 6)) = 1 + 4 + 9 = 14

**Constraints:**

-   `1 <= n <= 7`
-   `nums.length == 2 * n`
-   `1 <= nums[i] <= 106`

## Solution

### Recursive memoization with bit-masking

![[Pasted image 20230516152238.png]]

Idea:
- Backtrack through it by choosing every combination and find max value. 
- How to keep track of the element used? **Bit-masking**! This is basically keeping track of a visited array. However, bitmasking allows the use of [[Memoization]]!
- We can reach the same node through different paths. Hence we can memoize this node the first time we see it. The caching is the max value achieved from this node.
- How to find gcd? Use [[Euclid's GCD Algorithm]]

Time:
- Let m = 2n, hence m is the number of elements in nums array
- With memoization, we call the function O(2^m) times, which is the max number of states possible
- At each function call, we compute GCD of a pair of number, which takes O(lgA), where A is the max value of the number in the array.
- In each function call, we also have a nested for loop, which takes O(m^2)
- In total: `O(2^m * m^2 * lgA )`

Space:
- Recursion stack space: O(n)
- DP array: O(2^2n) = O(2^m) = O(4^n)

Optimization:
- Bottom-up DP (iterative)
- Cache all the possible GCD values (for some reason gave me different result?)


```python
'''
Bit-masking:

1. check if ith element is taken: mask & 1 << i
2. mark ith element: mask | 1 << i
'''
```


```python
class Solution:

    def gcd(self, a: int, b: int):
        if b == 0: 
            return a
        return gcd(b, a % b)

    def backtrack(self, nums, mask, mem, index):
        m = len(nums)
        n = m // 2

        if index > n:
            return 0
        
        if mem[mask] != -1: return mem[mask]

        for i in range(m):
            if mask & (1 << i): continue

            for j in range(i + 1, m):
                if mask & (1 << j): continue

                newMask = mask | 1 << i | 1 << j
                newVal = index * self.gcd(nums[i], nums[j]) +
	                self.backtrack(nums, newMask, mem, index + 1)
                mem[mask] = max(mem[mask], newVal)

        return mem[mask]

    def maxScore(self, nums: List[int]) -> int:
        m = len(nums)
        n = m // 2
        mem = [-1] * (1 << m) # 2 ^ m
        return self.backtrack(nums, 0, mem, 1)
```

---
Link: [[LeetCode]]
