---
tags:
  - LeetCode
  - leetcode
topics: BFS, SSSP
difficulty: hard
performance: complete, onTime
date: 2023-09-18 Monday
---

## Questions

You have an undirected, connected graph of `n` nodes labeled from `0` to `n - 1`. 

You are given an array `graph` where `graph[i]` is a list of all the nodes connected with node `i` by an edge.

Return _the length of the shortest path that visits every node_. You may start and stop at any node, you may revisit nodes multiple times, and you may reuse edges.

## Solution

### BFS

Big idea:
- Since we are allowed to revisit nodes, we need to keep track of state through a mask to avoid visiting the same node on the same path
- Naturally, we use BFS to find the shortest distance from state 0 to the final state. 

```python
class Solution:
    def shortestPathLength(self, graph: List[List[int]]) -> int:
        n = len(graph)
        seen = set()
        frontier = []

        for i in range(n):
            state = (1 << i)
            frontier.append((i, state))
            seen.add((i, state))

        goal_state = (1 << n) - 1
        distance = 0
        while frontier:
            next_frontier = []
            for node, state in frontier:
                if state == goal_state:
                    return distance

                for neighbor in graph[node]:
                    new_state = state | (1 << neighbor)
                    if (neighbor, new_state) in seen:
                        continue
                    next_frontier.append((neighbor, new_state))
                    seen.add((neighbor, new_state))

            frontier = next_frontier
            distance += 1
```

Time: O(N x 2^N)
- There are (N x 2^N) nodes

Space: O(N x 2^N)

---
Link: [[LeetCode]]
