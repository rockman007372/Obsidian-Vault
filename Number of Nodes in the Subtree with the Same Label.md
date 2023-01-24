---
tags: LeetCode
topics: tree, search, DFS
difficulty: medium
performance:
date: 2023-01-13 Friday
---

## Questions



## Solution

### DFS

Idea:
- Do a DFS on the tree.
- At each node, return a count array counting the number of letters in its subtree rooted at that node.

Time: O(26N) = O(N) as we add the count at each node which takes O(26) = O(1) time
	Space: O(N) recursion + O(26 * N) space

```python
class Solution:
    def countSubTrees(self, n: int, edges: List[List[int]], labels: str) -> List[int]:
        visited = [False] * n
        ans = [0] * n

        def count(root):
            """
            return an array of size 26, counting the number of letters in the subtree
            """
            nonlocal ans
            nonlocal visited

            visited[root] = True # mark as visited
            counter = [0] * 26
            
            # add label of root node
            label = ord(labels[root]) - ord('a')
            counter[label] += 1

            for neighbour in adjList[root]:

                if visited[neighbour]:
                    continue

                subCounter = count(neighbour)
                counter = [x + y for x, y in zip(counter, subCounter)]

            # modify the answer
            ans[root] = counter[label]

            return counter 

        # Create an adjacency list
        adjList = {}
        for edge in edges:
            a, b = edge
            if a not in adjList:
                adjList[a] = []
            if b not in adjList:
                adjList[b] = []
            adjList[a].append(b)
            adjList[b].append(a)

        count(root=0)
        return ans 
```

### Optimization

- We dont need to keep creating new count array. We can find the difference in the number of character before and after visiting a node to get how many characters are in that subtree rooted in that node.
- We dont need a visited array for DFS, just track the parent will do.

```python
class Solution:
    def countSubTrees(self, n: int, edges: List[List[int]], labels: str) -> List[int]:      
        graph = [[] for _ in range(n)]
        for a, b in edges:
            graph[a].append(b)
            graph[b].append(a)
            
        counts = [0] * len(string.ascii_lowercase)
        answer = [0] * n
        
        def dfs(node, parent):
            index = ord(labels[node]) - ord('a')
            previous = counts[index]
            counts[index] += 1
            
            for child in graph[node]:
                if child != parent:
                    dfs(child, node)
                    
            answer[node] = counts[index] - previous
        
        dfs(0, -1)
        return answer
```