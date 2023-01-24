2022-06-05 16:44
Tags: [[LeetCode]] - [[Binary Tree]] - [[Recursion]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
### Questions
Input: Binary Tree
Output: Max path sum (path does not have to go through root)

### Solution
Very similar idea to [[Diameter of Binary Tree]].

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
    int maxSum = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        maxHelper(root);
        return maxSum;
    }
    
    // return max sum along either branch
    public int maxHelper(TreeNode root) {
        if (root == null) {
            return 0;
        }
        
        // if the max of a branch is negative, we can ignore that branch
        // because it will only make the overall sum smaller
        int leftMax = Math.max(maxHelper(root.left), 0);
        int rightMax = Math.max(maxHelper(root.right), 0);
        
        // check if sum is greater if path follows 2 branches
        maxSum = Math.max(maxSum, leftMax + root.val + rightMax);
        
        // if path dont follow through both branches,
        // we have to go through either branches
        return Math.max(leftMax, rightMax) + root.val;
    }   
}
```

Time: O(N)
Space: O(h) = O(N)