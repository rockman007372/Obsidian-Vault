---
tags: LeetCode
topics: BFS, SSSP
difficulty: medium
performance: complete, notOnTime
date: 2023-01-17 Tuesday
---

## Questions

Given an `n x n` binary matrix `grid`, return _the length of the shortest **clear path** in the matrix_. If there is no clear path, return `-1`.

A **clear path** in a binary matrix is a path from the **top-left** cell (i.e., `(0, 0)`) to the **bottom-right** cell (i.e., `(n - 1, n - 1)`) such that:

-   All the visited cells of the path are `0`.
-   All the adjacent cells of the path are **8-directionally** connected (i.e., they are different and they share an edge or a corner).

The **length of a clear path** is the number of visited cells of this path.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/18/example1_1.png)

```
**Input:** grid = [[`0,1],[1,0`]]
**Output:** 2
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/18/example2_1.png)

```
**Input:** grid = `[[0,0,0],[1,1,0],[1,1,0]]`
**Output:** 4
```

## Solution

### BFS

Nothing too special, just standard BFS. Takeaways:
- Careful of distance edge cases (off by 1)
- Check for visited nodes and check for goal node BEFORE pushing into queue to save space and time.

```python
class Solution:
    def shortestPathBinaryMatrix(self, grid: List[List[int]]) -> int:
        
        n = len(grid)

        # no start or end
        if grid[0][0] != 0 or grid[n - 1][n - 1] != 0:
            return -1
        
        # if only 1 cell 0
        if n == 1:
            return 1


        # perform bfs to get SSSP from top left to bottom right
        # from (0, 0) to (n - 1, n - 1)
        root = (0, 0)
        frontier = [root]

        # visited set
        visited = set()
        visited.add(root)

        DIR = [
            [1, 0],
            [-1, 0],
            [0, 1],
            [0, -1],
            [1, 1],
            [1, -1],
            [-1, 1],
            [-1, -1]
        ]

        dist = 1
        while frontier:
            next_frontier = []

            for node in frontier:
                for direction in DIR:
                    r, c = node[0] + direction[0], node[1] + direction[1]
                    
                    if r >= 0 and c >= 0 and r < n and c < n: 
                        if (r, c) not in visited and grid[r][c] == 0:
                            
                            if (r, c) == (n - 1, n - 1): # check for goal node before pushing
                                return dist + 1

                            visited.add((r, c))
                            next_frontier.append((r, c))

            frontier = next_frontier
            dist += 1

        return -1 # if reach here, no path
```

---
Link: [[SSSP]], [[LeetCode]], [[Breadth First Search]]