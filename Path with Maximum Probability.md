---
tags: LeetCode, leetcode
topics: SSSP
difficulty: medium
performance: complete, suboptimal
date: 2023-06-28 Wednesday
---

## Questions

You are given an undirected weighted graph of `n` nodes (0-indexed), represented by an edge list where `edges[i] = [a, b]` is an **undirected** edge connecting the nodes `a` and `b` with a probability of success of traversing that edge `succProb[i]`.

Given two nodes `start` and `end`, find the path with the maximum probability of success to go from `start` to `end` and return its success probability.

If there is no path from `start` to `end`, **return 0**. Your answer will be accepted if it differs from the correct answer by at most **1e-5**.

## Solution

### Bellman-Ford

[[Bellman-Ford SSSP]] allows us to find the shortest distance between a source and any point. How to turn this into an SSSP problem with no negative edges? 

```
P = p1 * p2 * ... pn

logP = lgP1 + lgP2 + ...

-lgP = -lgP1 - lgP2 -...
```

Hence to find max(P), we find min(-lgP). Since p are probablities, p < 1, hence lgP < 0, hence -lgP > 0.

Notice that the edges are undirected. Hence we must relax the edges both way!!

```python
class Solution:
    def maxProbability(self, 
	    n: int, edges: List[List[int]], succProb: List[float], 
	    start: int, end: int) -> float:
        
        # Apply bellman-ford, relax in random order
        estimate = [float('inf')] * n
        estimate[start] = 0

        for _ in range(n - 1):
            changes = 0
            for ((u, v), prob) in zip(edges, succProb):
                prob = -math.log(prob)
                if estimate[v] > estimate[u] + prob:
                    estimate[v] = estimate[u] + prob
                    changes += 1

                if estimate[u] > estimate[v] + prob:
                    estimate[u] = estimate[v] + prob
                    changes += 1
            if not changes:
                    break

        if estimate[end] == float('inf'):
            return 0

        return math.e ** (-estimate[end])
```

Time: O(VE)
Space: O(V)

#### Optimization

In fact, you do not have to perform log operation at all. We establish that finding maximum probability P is equivalent to finding min -lgP. Hence we can directly modify the relax function to update the estimate whenever the product increases, and **directly** find the max product.

```python
class Solution:
    def maxProbability(self, n: int, edges: List[List[int]], succProb: List[float], start: int, end: int) -> float:
        max_prob = [0] * n    # or float('-inf')
        max_prob[start] = 1   # instead of 0
        
        for i in range(n - 1):
            has_update = 0
            
            for j in range(len(edges)):
                u, v = edges[j]
                path_prob = succProb[j]
                if max_prob[u] * path_prob > max_prob[v]:
                    max_prob[v] = max_prob[u] * path_prob
                    has_update = 1 
                if max_prob[v] * path_prob > max_prob[u]:
                    max_prob[u] = max_prob[v] * path_prob
                    has_update = 1
                
            if not has_update:
                break
        
        return max_prob[end]
```

### Djikstra

[[Dijkstra's Algorithm]]

Time: O(ElgV)
Space: O(V + E)

```python
class Solution:
    def maxProbability(self, n: int, edges: List[List[int]], succProb: List[float], start: int, end: int) -> float:

		# build graph
        graph = defaultdict(list)
        for i, (u, v) in enumerate(edges):
            graph[u].append((v, succProb[i]))
            graph[v].append((u, succProb[i]))
        
        max_prob = [0.0] * n
        max_prob[start] = 1.0

		# Djikstra
        pq = [(-1.0, start)]    # negate because pq is min heap
        while pq:
            cur_prob, cur_node = heapq.heappop(pq)
            if cur_node == end:
                return -cur_prob
            for nxt_node, path_prob in graph[cur_node]:

                if -cur_prob * path_prob > max_prob[nxt_node]:
                    max_prob[nxt_node] = -cur_prob * path_prob
                    heapq.heappush(pq, (-max_prob[nxt_node], nxt_node))
        return 0.0
```

---
Link: [[LeetCode]]
