---
tags: LeetCode, leetcode
topics: binaryTrees, dp, memoization
difficulty: medium
performance: complete, optimal
date: 2023-07-23 Sunday
---

## Questions

Given an integer `n`, return _a list of all possible **full binary trees** with_ `n` _nodes_. Each node of each tree in the answer must have `Node.val == 0`.

Each element of the answer is the root node of one possible tree. You may return the final list of trees in **any order**.

A **full binary tree** is a binary tree where each node has exactly `0` or `2` children.

## Solution

Observation:
- All full binary trees must have odd number of nodes.
- Each FBT are made up of FBTs => optimal and overlapping substructure

Time: `O(2 ^ (n / 2)) `
- ? The number of FBTs are bounded by `O(2 ^ n / 2) `
- Recursive relation: `O(n) = O(1) x O(n - 2) + O(3) x O(n - 4) + ...`, which equals the [[Catalan Number]]?

Space: `O(n * 2 ^ (n / 2))`

### Memoization

```python
class Solution:
    @cache
    def allPossibleFBT(self, n: int) -> List[Optional[TreeNode]]:
        if n % 2 == 0:
            return []

        if n == 1:
            return [TreeNode(0)]
        
        
        res = []
        for i in range(1, n, 2):
            for leftNode in self.allPossibleFBT(i):
                for rightNode in self.allPossibleFBT(n - 1 - i):
                    root = TreeNode(0)
                    root.left = leftNode
                    root.right = rightNode
                    res.append(root)
        
        return res
```

### DP

```python
class Solution:
    def allPossibleFBT(self, n: int) -> List[Optional[TreeNode]]:
        
        if n % 2 == 0:
            return []

        dp = {}
        dp[1] = [TreeNode(0)]
        for i in range(3, n + 1, 2):
            res = []
            for j in range(1, i, 2):
                leftTrees = dp[j]
                rightTrees = dp[i - j - 1]
                for leftNode in leftTrees:
                    for rightNode in rightTrees:
                        root = TreeNode(0, leftNode, rightNode)
                        res.append(root)
            dp[i] = res

        return dp[n]
```


---
Link: [[LeetCode]]
