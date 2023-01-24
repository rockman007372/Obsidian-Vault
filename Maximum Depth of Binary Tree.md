---
tags: LeetCode 
aliases: 
topics: binaryTree
difficulty: easy
performance:
---
Links: [[LeetCode]], [[Binary Tree]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

### Questions
Input: Binary tree
Output: Max depth

> Max depth of a tree = number of nodes along the *longest path* from the root node down to the farthest leaf node.

![[Maximum Depth of Binary Tree 2022-06-25 22.19.33.excalidraw]]

### Solution
```Java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        return Math.max(left, right) + 1;
    }
}
```