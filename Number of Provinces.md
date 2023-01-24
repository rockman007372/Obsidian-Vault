---
tags: LeetCode
topics: DFS, BFS
difficulty: medium
performance: complete, optimal
date: 2023-01-14 Saturday
---

## Questions

There are `n` cities. Some of them are connected, while some are not. If city `a` is connected directly with city `b`, and city `b` is connected directly with city `c`, then city `a` is connected indirectly with city `c`.

A **province** is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an `n x n` matrix `isConnected` where `isConnected[i][j] = 1` if the `ith` city and the `jth` city are directly connected, and `isConnected[i][j] = 0` otherwise.

Return _the total number of **provinces**_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/12/24/graph1.jpg)

**Input:** isConnected = `[[1,1,0],[1,1,0],[0,0,1]]`
**Output:** `2`

## Solution

Big idea: Basically traversing the graph using either DFS or BFS using an Adjacency Matrix (see [[Representing a Graph]])

### BFS
[[Breadth First Search]]

Key takeaways:
- Using 2 frontiers to avoid popping the head of the list which may takes O(N) time
- Check for duplicate before pushing into the frontier to reduce runtime (one fewer frontier to check)

```python
class Solution:
    def findCircleNum(self, isConnected: List[List[int]]) -> int:
        if not isConnected:
            return 0
            
        n = len(isConnected)
        visited = set()
        count = 0
        for node in range(n):
            if node not in visited: 
                count += 1
                
                # bfs
                frontier = [node]
                visited.add(node)
                while frontier:
                    new_frontier = []
                    for curr in frontier:
                        for neighbor, edge in enumerate(isConnected[curr]):
                            if neighbor in visited:
                                continue
                            if edge: # if edge == 1
                                visited.add(neighbor)
                                new_frontier.append(neighbor)
                    frontier = new_frontier
        return count

"""
Idea: 
do a bfs/dfs on each node 
if a node is not visited, increment count
"""
```

Time: O(N^2)
Space: O(N) to store visited hash set

