2022-06-05 16:44
Tags: [[LeetCode]] - [[Binary Tree]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Balanced Binary Tree
## My Performance


## Questions
Difficulty: #easy
Input: Binary Tree root
Output: Whether tree is balanced

## Solution
#### Top Down Recursion
For each node, we have to find height for O(h) times = O(N) times.
Time: O(N^2)

#### Bottom Up Recursion
Time: O(N)
Space: O(N)

```Java
class Solution {
    public boolean isBalanced(TreeNode root) {
        return height(root) != -2;  
    }
    
    // return -2 if tree is unbalanced, else
    // return the height of the tree
    public int height(TreeNode root) {
        if (root == null) return -1;
        
        int leftH = height(root.left);
        if (leftH == -2) return -2;
        
        int rightH = height(root.right);
        if (rightH == -2) return -2;
        
        // return -2 if a subtree is out of balance
        if (Math.abs(leftH - rightH) > 1) return -2;
        
        return Math.max(leftH, rightH) + 1;
    }
}
```