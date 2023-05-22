---
tags: LeetCode, leetcode
topics: graph
difficulty: medium
performance: uncomplete
date: 2023-05-19 Friday
---

## Questions

There is an **undirected** graph with `n` nodes, where each node is numbered between `0` and `n - 1`. You are given a 2D array `graph`, where `graph[u]` is an array of nodes that node `u` is adjacent to. More formally, for each `v` in `graph[u]`, there is an undirected edge between node `u` and node `v`. The graph has the following properties:

-   There are no self-edges (`graph[u]` does not contain `u`).
-   There are no parallel edges (`graph[u]` does not contain duplicate values).
-   If `v` is in `graph[u]`, then `u` is in `graph[v]` (the graph is undirected).
-   The graph may not be connected, meaning there may be two nodes `u` and `v` such that there is no path between them.

A graph is **bipartite** if the nodes can be partitioned into two independent sets `A` and `B` such that **every** edge in the graph connects a node in set `A` and a node in set `B`.

Return `true` _if and only if it is **bipartite**_.

Example: 

![](https://assets.leetcode.com/uploads/2020/10/21/bi1.jpg)

**Input:** graph = `[[1,3],[0,2],[1,3],[0,2]]`
**Output:** true
**Explanation:** We can partition the nodes into two sets: {0, 2} and {1, 3}.

## Solution

Idea: 
- Do a BFS/DFS on the graph, coloring them alternately as you go from on frontier to another. 
- If the color of a neighbor ever matches the color of the current node, there is an edge within an independent set. Hence it is not an bipartite graph. 
- There may be disconnected components, hence we must check every single nodes.
- Bipartite graph != complete bipartite graph. Bipartite graph definition: Divide the vertices in two independent sets such that **if any edges exists**, they exists between the nodes in two sets and not within each set.

Time: O(V + E)
- V is the number of vertices and E is the number of edges

Space: O(V)
- Stack size O(V)

```python
class Solution:
    def isBipartite(self, graph: List[List[int]]) -> bool:
        n = len(graph)
        color = {}
    
        # Iterative DFS - coloring approach
        for node in range(n):
            if node not in color:
                color[node] = 0
                stack = [node]  

                while stack:
                    curr = stack.pop()
                    for node in graph[curr]:

                        if node in color:
                            if color[node] == color[curr]:
                                return False
                            continue

                        color[node] = color[curr] ^ 1 # xor
                        stack.append(node)

        return True
```


---
Link: [[LeetCode]]
