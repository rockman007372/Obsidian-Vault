---
tags: LeetCode, leetcode
topics: dp, slidingWindow
difficulty: medium
performance: uncomplete
date: 2023-05-25 Thursday
---

## Questions

Alice plays the following game, loosely based on the card game **"21"**.

Alice starts with `0` points and draws numbers while she has less than `k` points. During each draw, she gains an integer number of points randomly from the range `[1, maxPts]`, where `maxPts` is an integer. Each draw is independent and the outcomes have equal probabilities.

Alice stops drawing numbers when she gets `k` **or more points**.

Return the probability that Alice has `n` or fewer points.

Answers within `10-5` of the actual answer are considered accepted.

## Solution

### DP 

Hardest challenge is to identify this is a DP problem.

Framework:
- DP state: `dp[i]` is the probability of getting i at any point
- Base case: `dp[0] = 1` since you always start with 0
- Recursive relation: `dp[i] = sum(dp[j]) / maxPts` where j is between `[max(i - j, 0), min(i - j, k - 1)]`
- Result = `sum(dp[k : n + 1])`

```python
class Solution:
    def new21Game(self, n: int, k: int, maxPts: int) -> float:
        dp = [0] * (n + 1) # dp[i] is the probability of getting i at any point
        dp[0] = 1 # score = 0 initially
        for i in range(1, n + 1):
            for j in range(1, maxPts + 1):
                if i - j < k and i - j >= 0:
                    dp[i] += dp[i - j] / maxPts
        
        return sum(dp[k : n + 1])
```

Time: O(n * maxPts)
Space: O(n)

### DP (optimized)

Recognize that we dont have to keep summing up the previous probability. The sum can be kept as a variable, and we move the window appropriately to the right as we traverse through the array. This reduces the time to O(n).

Special edge case is when k = 0. In that case, score is already reached before we play. `dp[i]` where i > 0 is always 0.

```python
class Solution:
    def new21Game(self, n: int, k: int, maxPts: int) -> float:
        dp = [0] * (n + 1)  # dp[i] = probability of scoreing i at anytime
        dp[0] = 1           # score = 0 initially
        
        sum_window = dp[0] if k != 0 else 0
        for i in range(1, n + 1):
            dp[i] = sum_window / maxPts

            if i < k:
                sum_window += dp[i]
            
            if i - maxPts >= 0 and i - maxPts < k:
                sum_window -= dp[i - maxPts]
    
        return sum(dp[k : n + 1])
```

---
Link: [[LeetCode]]
