---
tags: LeetCode, leetcode
topics: unionfind
difficulty: hard
performance: uncomplete
date: 2023-05-12 Friday
---

## Questions

Alice and Bob have an undirected graph of `n` nodes and three types of edges:

-   Type 1: Can be traversed by Alice only.
-   Type 2: Can be traversed by Bob only.
-   Type 3: Can be traversed by both Alice and Bob.

Given an array `edges` where `edges[i] = [typei, ui, vi]` represents a bidirectional edge of type `typei` between nodes `ui` and `vi`, find the maximum number of edges you can remove so that after removing the edges, the graph can still be fully traversed by both Alice and Bob. The graph is fully traversed by Alice and Bob if starting from any node, they can reach all other nodes.

Return _the maximum number of edges you can remove, or return_ `-1` _if Alice and Bob cannot fully traverse the graph._


## Solution

Idea: 
- Use [[Union-Find]] to eliminate unnecessary edges that join vertices in the same component. 
- Prioritize edges of type 3 (both can traverse) since this allow more edges to be removed. 

Time: O(NlgN)
- There are at most 3 * N edges to check
- Each union operation takes O(lgN) since we use UnionFind by weight/rank

Space: O(N)

```python
class UnionFind:
    componentNo = 0
    parents = []
    weights = [] # number of childrens

    def __init__(self, n: int):
        self.componentNo = n
        self.parents = [i for i in range(n + 1)]
        self.weights = [0] * (n + 1)

    def union(self, u: int, v: int):
        while u != self.parents[u]:
            u = self.parents[u]
        while v != self.parents[v]:
            v = self.parents[v]

        if u == v: # same component
            return False

        if self.weights[u] < self.weights[v]:
            self.parents[u] = v
            self.weights[v] += self.weights[u] + 1
        else:
            self.parents[v] = u
            self.weights[u] += self.weights[v] + 1

        self.componentNo -= 1
        return True

class Solution:

    def maxNumEdgesToRemove(self, n: int, edges: List[List[int]]) -> int:

        # prioritise type 3 edges by sorting in reverse
        sortedEdges = sorted(edges, key = lambda edge : edge[0], reverse = True)

        # Create 2 UF for A and B
        Alice = UnionFind(n)
        Bob = UnionFind(n)
        edgeRemoved = 0

        for edge in sortedEdges:
            edgeType, u, v = edge

            if edgeType == 3:
                if Alice.union(u, v):
                    Bob.union(u, v)
                    continue
                edgeRemoved += 1
            
            if edgeType == 2:
                if not Bob.union(u, v):
                    edgeRemoved += 1

            if edgeType == 1:
                if not Alice.union(u, v):
                    edgeRemoved += 1
            
        if Alice.componentNo != 1 or Bob.componentNo != 1:
            return -1
        
        return edgeRemoved

'''
input: number of nodes n : int, edges : list[[list[int]]]
output: the max number of edges removable such that both A and B can traverse every node on the graph.

assumptions:
- a graph is fully traversible if starting at ANY node, A and B can reach all the other nodes.
- an edge is bidirectional
'''
```

---
Link: [[LeetCode]]
