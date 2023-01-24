---
tags: LeetCode
topics: BFS, backtracking, DP
difficulty: medium
performance: complete
date: 2023-01-20 Friday
---

## Questions

Given a directed acyclic graph (**DAG**) of `n` nodes labeled from `0` to `n - 1`, find all possible paths from node `0` to node `n - 1` and return them in **any order**.

The graph is given as follows: `graph[i]` is a list of all nodes you can visit from node `i` (i.e., there is a directed edge from node `i` to node `graph[i][j]`).

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/28/all_1.jpg)

```
**Input:** graph = [[1,2],[3],[3],[]]
**Output:** [[0,1,3],[0,2,3]]
**Explanation:** There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/09/28/all_2.jpg)

```
**Input:** graph = [[4,3,1],[3,2,4],[3],[4],[]]
**Output:** [[0,4],[0,3,4],[0,1,3,4],[0,1,2,3,4],[0,1,4]]
```


## Solution

### BFS with history

Kinda like backtracking, but space is hugh as we have to keep track of all the space so far.

**Complexity Analysis**
- Time: `O((2^N) * N)`
	- There are possibly O(2^N) paths from 0 to N - 1.
	- Takes O(N) to append path to result.
- Space: `O(2^N * N)`? 

```python
class Solution:
    def allPathsSourceTarget(self, graph: List[List[int]]) -> List[List[int]]:

        n = len(graph) 

        root = (0, [0]) # node, history
        frontier = [root]
        res = []

        while frontier:
            next_frontier = []

            for node in frontier:
                val, history = node

                # Is this too costly?
                if val == (n - 1):
                    res.append(history)

                for neighborVal in graph[val]:
                    neighbor = (neighborVal, history + [neighborVal])
                    next_frontier.append(neighbor)

            frontier = next_frontier

        return res
```

### Backtracking

We employ [[Backtracking]] algo.

**Complexity Analysis**
- Time: `O((2^N) * N)`
	- There are possibly O(2^N) paths from 0 to N - 1.
	- Takes O(N) to append path to result.
- Space: `O(N)`
	- You only have to store the current path which is O(N) 

```python
class Solution:
    def allPathsSourceTarget(self, graph: List[List[int]]) -> List[List[int]]:

        n = len(graph) 
        res = []

        def backtrack(node: int, path: List[int]):
            if node == n - 1:
                res.append(list(path)) # make a new copy of path
            else:
                for neighbor in graph[node]:
                    path.append(neighbor)
                    backtrack(neighbor, path)
                    path.pop()

        backtrack(node=0, path=[0])
        return res
```

### DP

[[Dynamic Programming]] can be used here.
- `DP[i]` = all the paths to node `n - 1` from node `i`
- `DP[i]` = `[i] + DP[i+]` where `i+` are all the neighbor nodes of `i` 
- We can use some form of [[Memoization]]

```python
class Solution:
    def allPathsSourceTarget(self, graph: List[List[int]]) -> List[List[int]]:

        n = len(graph)
        
        def rPath(node: int):
            if node == n - 1:
                return [[node]]
            else:
                res = []
                for neighbor in graph[node]:
                    for path in rPath(neighbor):
                        res.append([node] + path)

                return res

        return rPath(0)
```
