---
tags: LeetCode
topics: Binary Tree
difficulty: easy
performance: complete
date: 2023-01-09 Monday
---

### Questions

Given the `root` of a binary tree, return _the preorder traversal of its nodes' values_.

### Solution

##### Recursive

```python
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        
        def helper(root, res):
            if not root:
                return
            else:
                res.append(root.val)
                helper(root.left, res)
                helper(root.right, res)
                
        res = []
        helper(root, res)
        return res
```

Time: O(N)
Space: O(N) due to recursive memory stack size

##### Iterative

Takeaway: order of adding children affects traversal order!

```python
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        
        if not root:
            return []

        # Iterative - using a stack to simulate DFS
        res = []
        frontier = []
        frontier.append(root)

        while frontier:
            curr = frontier.pop()
            
            if not curr:
                continue
            
            res.append(curr.val)
            frontier.append(curr.right) # add right child first!!
            frontier.append(curr.left)

        return res
```

Space: O(N) - Still need to store the nodes in stack!!

##### Approach 3: [[Morris Traversal]]

![[Pasted image 20230110000514.png]]

Algorithm:
1. Set root node as curr node
2. If curr node has a left child, find the rightmost leaf of the left subtree and mark it as last node.
3. Modify the last leaf node so that its right child is the curr node.
4. Recurse on the left subtree of the curr node.
5. Once we reach the last node, move to the right child and set its right child to NULL again. How do you know if we reach the last node? If the end node's right child is the curr node (cycle)

```python
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        answer = []
        curr = root
        
        while curr:
            # If there is no left child, go for the right child.
            # Otherwise, find the last node in the left subtree. 
            if not curr.left:
                answer.append(curr.val)
                curr = curr.right
            else:
                last = curr.left
                while last.right and last.right != curr:
                    last = last.right
                    
                # If the last node is not modified, we let 
                # 'curr' be its right child. Otherwise, it means we 
                # have finished visiting the entire left subtree.
                if not last.right:
                    answer.append(curr.val)
                    last.right = curr
                    curr = curr.left
                else:
                    last.right = None
                    curr = curr.right
        
        return answer
```

Time: O(N), each of the N - 1 edges is visited twice
Space: O(1)