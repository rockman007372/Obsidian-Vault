---
tags: LeetCode, leetcode
topics: 
difficulty:
performance: 
date: 2023-05-21 Sunday
---

## Questions

You are given an array of variable pairs `equations` and an array of real numbers `values`, where `equations[i] = [Ai, Bi]` and `values[i]` represent the equation `Ai / Bi = values[i]`. Each `Ai` or `Bi` is a string that represents a single variable.

You are also given some `queries`, where `queries[j] = [Cj, Dj]` represents the `jth` query where you must find the answer for `Cj / Dj = ?`.

Return _the answers to all queries_. If a single answer cannot be determined, return `-1.0`.

**Note:** The input is always valid. You may assume that evaluating the queries will not result in division by zero and that there is no contradiction.

**Example:**

```
Input: 
	equations = [["a","b"],["b","c"]], 
	values = [2.0, 3.0], 
	queries = [["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]

Output: [6.00000,0.50000,-1.00000,1.00000,-1.00000]
```


## Solution

### BFS solution

Big idea:
- The key is notice this is a graph question!
- Given a/b, b/c, a/c = a/b x b/c. Hence we can denote each letter as a node, and each division result as the weight of an edge.
- Notable python implementation: `defaultdict(defaultdict)` creates a dict with default value as a dict.

Time: O(N * M)
- Where N is the number of nodes and M is the number of queries

Space: O(N)
- BFS frontier has size of O(N)

```python
class Solution:
    def calcEquation(self, equations: List[List[str]], values: List[float], queries: List[List[str]]) -> List[float]:
        graph = defaultdict(defaultdict)
        
        # build graph: adj matrix? adj list? how to store values? \
        for equation, value in zip(equations, values):
            graph[equation[0]][equation[1]] = value
            graph[equation[1]][equation[0]] = 1 / value

        # for each queries, do a bfs/dfs on the first element
        result = []
        for query in queries:
            result.append(self.bfs(query, graph))
        return result

    def bfs(self, queries: List[List[str]], graph) -> float:
        num, denom = queries
        if num not in graph or denom not in graph:
            return -1.0

        root = (num, 1)
        frontier = [root]

        visited = set()
        visited.add(num)

        while frontier:
            nextFrontier = []
            for (node, product) in frontier:
                if node == denom:
                    return product
                
                for neighbor in graph[node]:
                    if neighbor in visited:
                        continue

                    neighborNode = (neighbor, product * graph[node][neighbor])
                    visited.add(neighbor)
                    nextFrontier.append(neighborNode)
            frontier = nextFrontier

        return -1.0
```

### Union Find

Idea:
- Use modified [[Union-Find]] with [[Path Compression]]
- For each node `id`, we stores its `root_id` and the relative weight of `id` with respect to its root `id`. 
- Given node `a` and `b`, we can find the ratio `a : b`  = relative weight of `a` : relative weight of `b`
- We adjust the weights lazily through the path compression in the `find` function 

```python
'''
component[id] -> [root_id, weight]

where: 
- root_id: root of the componenent id belongs to
- weight: the relative weight of id in relation to its root_id
- weight = id / root_id

Example:
a -> b <- c
a -> c = a / c = weight[a] / weight[c] = (a / b)  / (c / b)
'''
```

Time: O((N + M) x log N)
- N is number of equations, M is number of queries
- Max number of nodes = O(2N) = O(N)
- O(NLog N) to build the UF since each operation takes O(lgN) and there are N operations
- O(MLogN) to do query from the UF

Space: O(N)
- components and weights

```python
class UnionFind:

    def __init__(self, equations, values):
        
        self.components = {}
        self.weights = defaultdict(lambda: 1)

        for (dividend, divisor), value in zip(equations, values):

            # initialise components if necessary
            self.components.setdefault(dividend, dividend)
            self.components.setdefault(divisor, divisor)

            self.union(dividend, divisor, value)
    
    # find root and do path compression, update weight along the way
    def find(self, variable):
        parent = self.components[variable]
        if variable != parent:
            self.components[variable] = self.find(parent) # recursively updates parent's weight and parent
            self.weights[variable] *= self.weights[parent] # update weight

        print(self.weights[variable])
        return self.components[variable]

    def union(self, dividend, divisor, quotient):

        rootA, weightA = self.find(dividend), self.weights[dividend]
        rootB, weightB = self.find(divisor), self.weights[divisor]

        # union if not in the same component
        if rootA != rootB:
            self.components[rootA] = rootB
            self.weights[rootA] = quotient * weightB / weightA # relative weight of rootA in terms of rootB

    # returns the ratio (dividend : divisor)
    def solve(self, query):
        dividend, divisor = query

        # nodes dont exist
        if dividend not in self.components or divisor not in self.components:
            return -1

        rootA, weightA = self.find(dividend), self.weights[dividend]
        rootB, weightB = self.find(divisor), self.weights[divisor]

        # not in the same component
        if rootA != rootB:
            return -1

        return weightA / weightB

class Solution:
    def calcEquation(self, equations: List[List[str]], values: List[float], queries: List[List[str]]) -> List[float]:

        # initialise uf
        uf = UnionFind(equations, values)

        # append answer
        ans = []
        for query in queries:
            ans.append(uf.solve(query))
        
        return ans
```


---
Link: [[LeetCode]]
