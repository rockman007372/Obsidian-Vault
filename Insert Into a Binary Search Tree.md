---
tags: LeetCode
topics: BST
difficulty: medium
performance: complete, onTime
date: 2023-01-12 Thursday
---

## Questions

You are given the `root` node of a binary search tree (BST) and a `value` to insert into the tree. Return _the root node of the BST after the insertion_. It is **guaranteed** that the new value does not exist in the original BST.

**Notice** that there may exist multiple valid ways for the insertion, as long as the tree remains a BST after insertion. You can return **any of them**.

## Solution

Do note that for all the solutions below, we do not care about maintaining a balanced tree. Else, we have to rotate and modify the tree after insertion.

### Recursion

Time: O(N)
Space: O(N)

```python
class Solution:
    def insertIntoBST(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:
        if not root:
            return TreeNode(val)
        
        if root.val > val:
            root.left = self.insertIntoBST(root.left, val)

        else:
            root.right = self.insertIntoBST(root.right, val)

        return root
```

### Iterative

Time: O(N)
Space: O(1)

```python
class Solution:
    def insertIntoBST(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:
        if not root:
            return TreeNode(val)
        
        curr = root
        while curr:
            if curr.val > val:
                if not curr.left:
                    curr.left = TreeNode(val)
                    break
                curr = curr.left
            else:
                if not curr.right:
                    curr.right = TreeNode(val)
                    break
                curr = curr.right
        
        return root
```