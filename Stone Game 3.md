---
tags: LeetCode, leetcode
topics: dp, memoization
difficulty: hard
performance: complete, notOnTime
date: 2023-05-27 Saturday
---

## Questions

Alice and Bob continue their games with piles of stones. There are several stones **arranged in a row**, and each stone has an associated value which is an integer given in the array `stoneValue`.

Alice and Bob take turns, with Alice starting first. On each player's turn, that player can take `1`, `2`, or `3` stones from the **first** remaining stones in the row.

The score of each player is the sum of the values of the stones taken. The score of each player is `0` initially.

The objective of the game is to end with the highest score, and the winner is the player with the highest score and there could be a tie. The game continues until all the stones have been taken.

Assume Alice and Bob **play optimally**.

Return `"Alice"` _if Alice will win,_ `"Bob"` _if Bob will win, or_ `"Tie"` _if they will end the game with the same score_.

## Solution

### Top-down Memoization

- f(i) returns the max number of stones that the starting player can get when there are (n - i) piles left
- Based on [[Stone Game 2]] solution.

Time: O(N)
Space: O(N)

```python
class Solution:
    def stoneGameIII(self, stoneValue: List[int]) -> str:
        n = len(stoneValue)

        def minimax(i):
            """
            i: the number of piles taken
            return: the max number of stones scored by the starting player,
            given that i piles have been taken
            """
            if i == n:
                return 0

            if memo[i] != -1:
                return memo[i]
            
            res = float("-inf")
            stonesAdded = 0
            for piles in range(1, min(n - i + 1, 4)): 
                stonesAdded += stoneValue[i + piles - 1]
                remainingSum = prefixSum[n - 1] - prefixSum[i + piles - 1]
                res = max(res, stonesAdded + remainingSum - minimax(i + piles))
            memo[i] = res
            return res
            

        memo = [-1 for _ in range(n)]

        # create prefixSum array
        prefixSum = [0] * n
        prefixSum[0] = stoneValue[0]
        for i in range(1, n):
            prefixSum[i] = prefixSum[i - 1] + stoneValue[i]


        AliceScore = minimax(0)
        BobScore = prefixSum[n - 1] - AliceScore

        if AliceScore > BobScore:
            return 'Alice'
        elif BobScore > AliceScore:
            return "Bob"
        else:
            return 'Tie'
```

### Bottom-up DP

- **State**: `dp[i] = difference between player x - player y`
- **Base case**: `dp[n] = 0`
- **Recursive relation**: `dp[i] = max(sum(values[i : i + piles]) - dp[i + piles]) for piles btw 1 and 3`

Time: O(N)
Space: O(N)

```python
class Solution:
    def stoneGameIII(self, stoneValue: List[int]) -> str:
        n = len(stoneValue)

        # stores the stone difference btw Alice and Bob 
        # when there are (n - i) piles left
        dp = [0] * (n + 1) # dp[n] = 0; there is no stone left

        for i in range(n - 1, -1, -1):
            stonesAdded = stoneValue[i]
            dp[i] = stonesAdded - dp[i + 1] 
            
            if i + 1 < n:
                stonesAdded += stoneValue[i + 1]
                dp[i] = max(dp[i], stonesAdded - dp[i + 2])

            if i + 2 < n:
                stonesAdded += stoneValue[i + 2]
                dp[i] = max(dp[i], stonesAdded - dp[i + 3])

        if dp[0] > 0:
            return "Alice"
        if dp[0] < 0:
            return "Bob"
        return "Tie"
```

### Bottom-up DP with optimized space

- Realise that `dp[i]` only relies on `dp[i +1]`, `dp[i +2]` and `dp[i + 3]`. Hence we only need an array of size 4.
- ! How to loop through the array? Use **modulo**! eg. `dp[i % 4]`
- Notice we still check `dp[0]` at the end. `dp[i]` stills represent the same state (difference btw 1st and 2nd player after taking i piles). At the end, `dp[0]` still represents the difference after taking 0 piles.
- Space: O(1)

```python
class Solution:
    def stoneGameIII(self, stoneValue: List[int]) -> str:
        n = len(stoneValue)

        # stores the stone difference btw 1st and 2nd player,
        # at (n - i) piles left

        # initialise dp
        dp = [0] * 4

        for i in range(n - 1, -1, -1):
            stonesAdded = stoneValue[i]
            dp[i % 4] = stonesAdded - dp[(i + 1) % 4] 
            
            if i + 1 < n:
                stonesAdded += stoneValue[i + 1]
                dp[i % 4] = max(dp[i % 4], stonesAdded - dp[(i + 2) % 4])

            if i + 2 < n:
                stonesAdded += stoneValue[i + 2]
                dp[i % 4] = max(dp[i % 4], stonesAdded - dp[(i + 3) % 4])

        if dp[0] > 0:
            return "Alice"
        if dp[0] < 0:
            return "Bob"
        return "Tie"
```


---
Link: [[LeetCode]]
