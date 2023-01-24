---
tags: LeetCode
topics: Binary Tree, Binary Search Tree
difficulty: medium
performance: complete
date: 2023-01-11 Wednesday
---

Very similar question to [[Construct Binary Tree from Preorder and Inorder Traversal]]

## Questions

Given an array of integers preorder, which represents the **preorder traversal** of a BST (i.e., **binary search tree**), construct the tree and return _its root_.

It is **guaranteed** that there is always possible to find a binary search tree with the given requirements for the given test cases.

A **binary search tree** is a binary tree where for every node, any descendant of `Node.left` has a value **strictly less than** `Node.val`, and any descendant of `Node.right` has a value **strictly greater than** `Node.val`.

A **preorder traversal** of a binary tree displays the value of the node first, then traverses `Node.left`, then traverses `Node.right`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/03/06/1266.png)

```
Input: preorder = [8,5,1,7,10,12]
Output: [8,5,10,1,7,null,12]
```

## Solution

### Recursion

Key idea:
- Build tree recursively
- Keep track of left and right indices instead of slicing the whole array

```python
class Solution:
    def bstFromPreorder(self, preorder: List[int]) -> Optional[TreeNode]:

        def buildBTS(left, right):

            if left > right:
                return None

            rootVal = preorder[left]
            root = TreeNode(rootVal)

            pointer = left
            while pointer + 1 <= right and preorder[pointer + 1] < rootVal:
                pointer += 1
            
            leftTree = buildBTS(left + 1, pointer)
            rightTree = buildBTS(pointer + 1, right)

            root.left = leftTree
            root.right = rightTree

            return root

        return buildBTS(0, len(preorder) - 1)
```

Time: O(N)
Space: O(N) - Recursion stack space

##### Construct Inorder Traversal of BST

Interesting idea: Inorder Traversal of a BST is an array sorted in ascending order.

Hence, we can sort the preorder array in `O(NlgN)` then construct the tree just like [[Construct Binary Tree from Preorder and Inorder Traversal]]

### Iterative

Convert the recursion solution to iterative with the help of a stack.

**Algorithm**

The recursion above could be converted into the iteration with the help of stack.

-   Pick the first preorder element as a root `root = new TreeNode(preorder[0])` and push it into stack.
    
-   Use `for` loop to iterate along the elements of preorder array :
    
    -   Pick the last element of the stack as a parent node, and the the current element of preorder as a child node.
        
    -   Adjust the parent node : pop out of stack all elements with the value smaller than the child value. Change the parent node at each pop `node = stack.pop()`.
        
    -   If `node.val < child.val` - put the child as a right child of the node : `node.right = child`.
        
    -   Else - as a left child : `node.left = child`.
        
    -   Push child node into the stack.
        
-   Return `root`.

```python
class Solution:
    def bstFromPreorder(self, preorder: List[int]) -> TreeNode:
        n = len(preorder)
        if not n:
            return None
        
        root = TreeNode(preorder[0])         
        stack = [root, ] 
        
        for i in range(1, n):
            # take the last element of the stack as a parent
            # and create a child from the next preorder element
            node, child = stack[-1], TreeNode(preorder[i])
            # adjust the parent 
            while stack and stack[-1].val < child.val: 
                node = stack.pop()
             
            # follow BST logic to create a parent-child link
            if node.val < child.val:
                node.right = child 
            else:
                node.left = child 
            # add the child into stack
            stack.append(child)
  
        return root
```