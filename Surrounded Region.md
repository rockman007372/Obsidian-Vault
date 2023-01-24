---
tags: LeetCode
topics: DFS, BFS
difficulty: medium
performance: uncomplete
date: 2023-01-17 Tuesday
---

## Questions

Given an `m x n` matrix `board` containing `'X'` and `'O'`, _capture all regions that are 4-directionally surrounded by_ `'X'`.

A region is **captured** by flipping all `'O'`s into `'X'`s in that surrounded region.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/xogrid.jpg)

**Input:** board = `[["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]`
**Output:** `[["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]`
**Explanation:** Notice that an 'O' should not be flipped if:
- It is on the border, or
- It is adjacent to an 'O' that should not be flipped.
The bottom 'O' is on the border, so it is not flipped.
The other three 'O' form a surrounded region, so they are flipped.

**Example 2:**

**Input:** board = `[["X"]]`
**Output:** `[["X"]]`

## Solution

### DFS + Escape strategy


Idea:
- Only do DFS on the border entries. Mark all the entries visited as "E", as they all escape and cannot be contained
- Modify board in place so all unchanged Os become Xs and all E becomes Os.
- Time: O(N)
- Space: O(N) - recursion depth

```python
class Solution:
    def solve(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        DIRS = [[1, 0], [-1, 0], [0, 1], [0, -1]]

        def dfs(r, c):
            if r >= 0 and c >= 0 and r < ROWS and c < COLS:
                if board[r][c] == 'X' or board[r][c] == 'E':
                    return
                else: # entry == O
                    board[r][c] = 'E'
                    for direction in DIRS:
                        dfs(r + direction[0], c + direction[1])
                    
        if not board:
            return board

        ROWS, COLS = len(board), len(board[0])

        # Do a DFS on each border entries to find all the escape entries

        # All border rows
        for r in (0, ROWS - 1):
            for c in range(COLS):
                dfs(r, c)

        # ALL border columns
        for c in (0, COLS - 1):
            for r in range(ROWS):
                dfs(r, c)

        # Modify every entry if necessary
        for r in range(ROWS):
            for c in range(COLS):
                if board[r][c] == 'O': board[r][c] = 'X'
                if board[r][c] == 'E': board[r][c] = 'O'

        return board
```

**Slight optimizations:**

> Rather than doing the boundary check within the `DFS()` function, we do it _**before**_ the invocation of the function.

```python
def DFS(self, board, row, col):
        if board[row][col] != 'O':
            return
        board[row][col] = 'E'
        if col < self.COLS-1: self.DFS(board, row, col+1)
        if row < self.ROWS-1: self.DFS(board, row+1, col)
        if col > 0: self.DFS(board, row, col-1)
        if row > 0: self.DFS(board, row-1, col)
```

_This measure reduces the number of recursion, therefore it reduces the overheads with the function calls._

As trivial as this modification might seem to be, it actually reduces the runtime of the Python implementation from _148 ms_ to _124 ms_, _i.e._ _16%_ of reduction, which beats 97% of submissions instead of 77% at the moment.


### BFS to reduce space complexity

Alternatively, we can replace DFS with BFS. This will reduce the space complexity from O(MN) to O(M + N), which is the maximum size of the queue at any time to hold the nodes in one frontier.

Why? Since in the problem we always start at border, max size of the queue will be the diagonal, which is less than M + N by triangle inequality. 

![[Pasted image 20220616135058.png]]

In fact, a closer upper bound would be `min(numRows, numCols)` or `O(min(M, N))`! Similar to [[Number of Islands]]

---
Link: [[Depth First Search]], [[Breadth First Search]]