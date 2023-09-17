---
tags:
  - LeetCode
  - leetcode
topics: binaryTree
difficulty: medium
performance: 
date: 2022-07-24 Sunday
---
[[Binary Tree]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
### Questions
Input: Root node of a binary tree
Output: Diameter of the tree
Diameter of a graph is the longest length (in the shortest path) between any 2 nodes in the graph.

### Solution - DFS

Time: O(N)
Space: O(N)

```Java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    private int diameter;
    public int diameterOfBinaryTree(TreeNode root) {
        diameter = 0;
        height(root);
        return diameter - 1; // -1 because we count edges not nodes
    }
    
	// update the diameter and return the height != depth of tree
    public int height(TreeNode node) {
        if (node == null) return 0;
        int left = height(node.left);
        int right = height(node.right);
        diameter = Math.max(diameter, left + right + 1);
        return Math.max(left, right) + 1;
    }
}
```

```python
class Solution:

    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        global diameter
        diameter = 0
		
		# update the diameter and return the height != depth of tree
        def helper(root):
            global diameter
            if not root:
                return 0
                
            left = helper(root.left)
            right = helper(root.right)
            
            diameter = max(diameter, right + left + 1)
            return max(right, left) + 1
        
        helper(root)
        return diameter - 1
```