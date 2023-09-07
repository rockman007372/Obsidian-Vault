---
tags: LeetCode, leetcode
topics: 
difficulty:
performance: complete, notOptimal
date: 2023-07-22 Saturday
---

## Questions

On an `n x n` chessboard, a knight starts at the cell `(row, column)` and attempts to make exactly `k` moves. The rows and columns are **0-indexed**, so the top-left cell is `(0, 0)`, and the bottom-right cell is `(n - 1, n - 1)`.

A chess knight has eight possible moves it can make, as illustrated below. Each move is two cells in a cardinal direction, then one cell in an orthogonal direction.

![](https://assets.leetcode.com/uploads/2018/10/12/knight.png)

Each time the knight is to move, it chooses one of eight possible moves uniformly at random (even if the piece would go off the chessboard) and moves there.

The knight continues moving until it has made exactly `k` moves or has moved off the chessboard.

Return _the probability that the knight remains on the board after it has stopped moving_.
## Solution

### Memoization

Note:
- Why divide by 8 at result? prob = prob(path1) / 8 + prob(path2) / 8 + ... = sum / 8
- Time: O(kn^2). Since we memoize the nodes, we expand each node at most 1 times. There are O(n x n x k) possible nodes. The removal of repeated nodes reduce the number of nodes from O(8 ^ k) to O(kn^2).
- Space: O(n x n x k) = O(kn^2)

```python
class Solution:
    def knightProbability(self, n: int, k: int, row: int, column: int) -> float:
        
        DIR = [
            [1, 2], [2, 1],
            [2, -1], [1, -2],
            [-1, -2], [-2, -1],
            [-2, 1], [-1, 2]
        ]

        # cache = {}

        @cache
        def dfs(r, c, level):
            # nonlocal cache

            if r < 0 or c < 0 or r >= n or c >= n:
                return 0
            
            # if (r, c, level) in cache:
            #     return cache[(r, c, level)]

            if level == k:
                return 1 

            res = 0
            for dir in DIR:
                x, y = r + dir[0], c + dir[1]
                res += dfs(x, y, level + 1)
            # cache[(r, c, level)] = res
            return res / 8
            
        return dfs(row, column, 0) 
```

## Bottom-up DP

```python
class Solution:
    def knightProbability(self, n: int, k: int, row: int, column: int) -> float:
        
        DIR = [
            [1, 2], [2, 1],
            [2, -1], [1, -2],
            [-1, -2], [-2, -1],
            [-2, 1], [-1, 2]
        ]

        dp = [[[0] * n for _ in range(n)] for _ in range(k + 1)]
        
    
        for step in range(k + 1):
            for r in range(n):
                for c in range(n):
                    
                    if step == 0:
                        dp[step][r][c] = 1
                    
                    else:
                        for dir in DIR:
                            x, y = r + dir[0], c + dir[1]
                            if x >= 0 and y >= 0 and x < n and y < n:
                                dp[step][r][c] += dp[step - 1][x][y]

                        dp[step][r][c] /= 8
        
        return dp[k][row][column]
```

Observe that we only need the probabilities from the previous move to calculate the probabilities for the current move! Hence we can reduce the space further to O(N^2):

```python
class Solution:
    def knightProbability(self, n: int, k: int, row: int, column: int) -> float:
        
        DIR = [
            [1, 2], [2, 1],
            [2, -1], [1, -2],
            [-1, -2], [-2, -1],
            [-2, 1], [-1, 2]
        ]

        dp = [[[0] * n for _ in range(n)] for _ in range(2)]
        
    
        for step in range(k + 1):
            for r in range(n):
                for c in range(n):
                    
                    # reset the cell!!
                    dp[step % 2][r][c] = 0

                    if step == 0:
                        dp[step % 2][r][c] = 1
                    
                    else:
                        for dir in DIR:
                            x, y = r + dir[0], c + dir[1]
                            if x >= 0 and y >= 0 and x < n and y < n:
                                dp[step % 2][r][c] += dp[(step - 1) % 2][x][y] 

                        dp[step % 2][r][c] /= 8
        
        return dp[k % 2][row][column]
```



---
Link: [[LeetCode]]
