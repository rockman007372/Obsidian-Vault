---
tags: LeetCode, leetcode
topics: bfs, dfs, graph
difficulty: medium
performance: complete, hinted
date: 2023-05-22 Monday
---

## Questions

You are given an `n x n` binary matrix `grid` where `1` represents land and `0` represents water.

An **island** is a 4-directionally connected group of `1`'s not connected to any other `1`'s. There are **exactly two islands** in `grid`.

You may change `0`'s to `1`'s to connect the two islands to form **one island**.

Return _the smallest number of_ `0`_'s you must flip to connect the two islands_.

**Example 1:**

**Input:** grid = `[[0,1],[1,0]]`
**Output:** 1

**Example 2:**

**Input:** grid = `[[0,1,0],[0,0,0],[0,0,1]]`
**Output:** 2

**Example 3:**

**Input:** grid = `[[1,1,1,1,1],[1,0,0,0,1],[1,0,1,0,1],[1,0,0,0,1],[1,1,1,1,1]]`
**Output:** 1

## Solution

## DFS + BFS

Idea:
- DFS to find the first island, and add the lands to the BFS frontier
- Starting from this frontier, BFS to find the next frontier. If we reach the next 2nd island in the next frontier, return the distance. Else increment the distance!

Time: O(N^2) = O(M), where M is the number of lands / nodes
Space: O(N^2) = O(M)

```python
class Solution:
    def shortestBridge(self, grid: List[List[int]]) -> int:
        n = len(grid)
        
        # find first land of the first island
        root = (0, 0)
        for i in range(n):
            found = False
            for j in range(n):
                if grid[i][j] == 1:
                    root = (i, j)
                    grid[i][j] = 2 # marked as visited
                    found = True  
                    break
            if found:
                break

        # prepare frontier for BFS
        frontier = [root]

        # dfs to find first island
        stack = [root]
        DIR = [(0, 1), (0, -1), (1, 0), (-1, 0)]
        while stack:
            curr_x, curr_y = stack.pop()
            for x, y in DIR:
                next_x = curr_x + x
                next_y = curr_y + y

                # if out of bounds
                if  next_x < 0 or next_x >= n or next_y < 0 or next_y >= n:
                    continue

                # if part of 1st island
                if grid[next_x][next_y] == 1: 
                    grid[next_x][next_y] = 2
                    stack.append((next_x, next_y))

                    # add all the lands in the first island to the current frontier
                    frontier.append((next_x, next_y)) 
        
        # BFS from the current frontier to the next frontier
        distance = 0
        while frontier:
            next_frontier = []

            for curr_x, curr_y in frontier:
                for x, y in DIR:
                    next_x, next_y = curr_x + x, curr_y + y

                    if  next_x < 0 or next_x >= n or next_y < 0 or next_y >= n:
                        continue
                    
                    # if already visited, skip
                    if grid[next_x][next_y] == 2: 
                        continue

                    # goal check: before pushing to save the checking of the last frontier
                    # found shortest path to 2nd island
                    if grid[next_x][next_y] == 1: 
                        return distance
                    
                    grid[next_x][next_y] = 2
                    next_frontier.append((next_x, next_y))
            
            frontier = next_frontier
            distance += 1

        return -1
```

---
Link: [[LeetCode]]
