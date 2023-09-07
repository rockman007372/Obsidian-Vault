---
tags: LeetCode, leetcode
topics: dp, memoization, gameTheory, minimax
difficulty: hard
performance: complete, notOnTime
date: 2023-05-26 Friday
---

## Questions

Alice and Bob continue their games with piles of stones.  There are a number of piles **arranged in a row**, and each pile has a positive integer number of stones `piles[i]`.  The objective of the game is to end with the most stones. 

Alice and Bob take turns, with Alice starting first.  Initially, `M = 1`.

On each player's turn, that player can take **all the stones** in the **first** `X` remaining piles, where `1 <= X <= 2M`.  Then, we set `M = max(M, X)`.

The game continues until all the stones have been taken.

Assuming Alice and Bob play optimally, return the maximum number of stones Alice can get.

**Example 1:**

**Input:** piles = `[2,7,9,4,4]`
**Output:** 10
**Explanation:**  If Alice takes one pile at the beginning, Bob takes two piles, then Alice takes 2 piles again. Alice can get 2 + 4 + 4 = 10 piles in total. If Alice takes two piles at the beginning, then Bob can take all three piles left. In this case, Alice get 2 + 7 = 9 piles in total. So we return 10 since it's larger.

## Solution

### Minimax with Memoization

This is a standard [[Minimax]] Problem. Each player tries to maximise their stones at the expense of the other player's stone.

Noteworthy points:
- The state of the game is (i, m), where i is the number of piles already taken, and m is the M stated in the question.
- Root node is (0, 1), and base node is (n, m). f(n, m) = 0 for any m. 
- To prevent memorizing the turn, treat the function as returning the max number of stones the STARTING player can get in that state

```python
class Solution:
    def stoneGameII(self, piles: List[int]) -> int:
        n = len(piles)
        def helper(i, m):
            """
            i: number of piles already taken
            m: M value in the game
            return: max number of stones STARTING player can get
            """
            if i == n:
                return 0
            
            if m in memo[i]:
                return memo[i][m]
            
            res = float("-inf") 
            stonesTaken = 0
            
            for x in range(1, min(2 * m, n - i) + 1):
                stonesTaken += piles[i + x - 1]
                remainingStones = 
	                prefSum[n - 1] - prefSum[i + x - 1]
                res = max(res, 
	                stonesTaken + 
	                remainingStones - helper(i + x, max(m, x)))
            
            memo[i][m] = res
            return res

        # calculate Prefix Sum
        prefSum = [0] * n
        prefSum[0] = piles[0]
        for i in range(1, n):
            prefSum[i] = prefSum[i - 1] + piles[i]

        # create memo table, with max m = n - 1 and max i = n - 1
        # memo = [[-1 * (n + 1)] for _ in range (n + 1)] 
        memo = defaultdict(defaultdict)

        return helper(0, 1) 
```

---
Link: [[LeetCode]]
