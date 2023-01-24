---
tags: LeetCode
topics: DynamicProgramming, Memoization
difficulty: medium
performance: [complete, optimal]
---
Date:: 2022-07-31 Sunday
Tags: [[LeetCode]] - [[Dynamic Programming]] - [[Memoization]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Unique Paths

### Questions
There is a robot on an `m x n` grid. The robot is initially located at the **top-left corner** (i.e., `grid[0][0]`). The robot tries to move to the **bottom-right corner** (i.e., `grid[m - 1][n - 1]`). The robot can only move either down or right at any point in time.

Given the two integers `m` and `n`, return _the number of possible unique paths that the robot can take to reach the bottom-right corner_.

![[Pasted image 20220801010815.png]]

Difficulty: #medium 
Input: `int` m and `int` n
Output: `int` number of paths 

### Solution
##### Top-Down Memoization
Time: O($2^{N + M}$) loosely -> With memoization: O(N * M)

![[Unique Paths 2022-08-01 01.32.16.excalidraw||800]]

Space: O(N * M)

```Java
class Solution {
    private int[][] cache;
    public int uniquePaths(int m, int n) {
        cache = new int[m][n];
        return pathHelper(m - 1, n - 1);
    }
    
    private int pathHelper(int r, int c) {
        if (r < 0 || c < 0) {
            return 0;
        }
        
        if (r == 0 && c == 0) {
            return 1;
        }
        
        if (cache[r][c] != 0) return cache[r][c];
        
        int result = pathHelper(r - 1, c) + pathHelper(r, c - 1);
        cache[r][c] = result;
        return cache[r][c];
    }
}
```

##### Bottom-Up Dynamic Programming
-   Time complexity: $\mathcal{O}(N \times M)$.
-   Space complexity: $\mathcal{O}(N \times M)$

```Java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] DP = new int[m][n];
        
        // fill the last column
        for (int r = 0; r < m; r++) {
            DP[r][n - 1] = 1;
        }
        
        // fill the last row
        for (int c = 0; c < n; c++) {
            DP[m - 1][c] = 1;
        }
        
        // DP from bottom
        for (int r = m - 2; r >= 0; r--) {
            for (int c = n - 2; c >= 0; c--) {
                DP[r][c] = DP[r + 1][c] + DP[r][c + 1];
            }
        }
        
        return DP[0][0];
    }
}
```