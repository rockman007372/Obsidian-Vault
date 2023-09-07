---
tags: LeetCode, leetcode
topics: dp
difficulty: hard
performance: uncomplete
date: 2023-06-12 Monday
---

## Questions

Given a wooden stick of length `n` units. The stick is labelled from `0` to `n`. For example, a stick of length **6** is labelled as follows:

![](https://assets.leetcode.com/uploads/2020/07/21/statement.jpg)

Given an integer array `cuts` where `cuts[i]` denotes a position you should perform a cut at.

**The cost of one cut is the length of the stick to be cut**. The total cost is the sum of costs of all cuts. When you cut a stick, it will be split into two smaller sticks (i.e. the sum of their lengths is the length of the stick before the cut). 

Return _the minimum total cost_ of the cuts.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/07/23/e1.jpg)

**Input:** n = 7, cuts = `[1,3,4,5]`
**Output:** 16

## Solution

### Top-down Memoization 

- DP state: `dp[i][j]` is the minimum cost of cutting between $i^{th}$ and $j^{th}$ cutting points.
- DP base case: `dp[i][i + 1] = 0` since there are no more cuts.
- DP recursive relation: `dp[i][j] = min(cuts[j] - cuts[i] + dp[i][cut] + dp[cut][j] for cut between the ith and jth cuts`

```python
class Solution:
    def minCost(self, n: int, cuts: List[int]) -> int:
        sorted_cuts = [0] + sorted(cuts) + [n]
        mem = {}

        def cost(lo: int, hi: int):
            if hi == lo + 1:
                return 0

            if (lo, hi) in mem:
                return mem[(lo, hi)]

            res = float('inf')
            for i in range(lo + 1, hi):
	            length = sorted_cuts[hi] - sorted_cuts[lo]
                res = min(res, length + cost(lo, i) + cost(i, hi))
            
            mem[(lo, hi)] = res
            return res
                
        return cost(0, len(sorted_cuts) - 1) 
```

Time: O(M^3)
- There are O(M^2) subproblems
- Each subproblem requires checking O(M) cuts 

Space: O(M^2)

### Bottom-up DP

To save the recursive stack, we can build the dp table starting from the base case. The base case is when there is no more cuts, i.e. `dp[i][i + 1]`. Then we move on to the case when there is only 1 cut... and repeat until we have all `m` cuts, where m is the number of cuts we have originally. 

```python
class Solution:
    def minCost(self, n: int, cuts: List[int]) -> int:
        sorted_cuts = [0] + sorted(cuts) + [n]
        m = len(sorted_cuts)
        dp = [[0 for _ in range(m)] for _ in range(m)]

        for diff in range(2, m):
            for lo in range(0, m):
                hi = lo + diff

                if hi >= m:
                    continue

                dp[lo][hi] = float('inf')
                for cut in range(lo + 1, hi):
                    dp[lo][hi] = min(dp[lo][hi], 
                        sorted_cuts[hi] - sorted_cuts[lo] + dp[lo][cut] + dp[cut][hi]) 

        return dp[0][m - 1]
```




---
Link: [[LeetCode]]
