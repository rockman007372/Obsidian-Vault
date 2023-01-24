---
tags: LeetCode, leetcode
topics: binary tree
difficulty: easy
performance: complete
date: 2022-07-24 Sunday
---

## Questions
Difficulty: #easy 
Input: Root and target sum
Output: Boolean whether the root-to-leaf sum is equal to target

## Solution
##### Recursion
Time and Space: O(N)

```Java
class Solution {
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if (root == null) return false;
        
        if (root.left == null && root.right == null) 
            return targetSum == root.val;
        
        int newTarget = targetSum - root.val;
        return hasPathSum(root.left, newTarget) || 
            hasPathSum(root.right, newTarget);
    }
}
```

##### Iterative DFS
Idea: Maintain 2 stacks to keep track of current nodes and the current path sum.

```Java
class Solution {
  public boolean hasPathSum(TreeNode root, int sum) {
    if (root == null)
      return false;

    LinkedList<TreeNode> node_stack = new LinkedList();
    LinkedList<Integer> sum_stack = new LinkedList();
    node_stack.add(root);
    sum_stack.add(sum - root.val);

    TreeNode node;
    int curr_sum;
    while ( !node_stack.isEmpty() ) {
      node = node_stack.pollLast();
      curr_sum = sum_stack.pollLast();
      if ((node.right == null) && (node.left == null) && (curr_sum == 0))
        return true;
    
    // go through each child
      if (node.right != null) {
        node_stack.add(node.right);
        sum_stack.add(curr_sum - node.right.val);
      }
      if (node.left != null) {
        node_stack.add(node.left);
        sum_stack.add(curr_sum - node.left.val);
      }
    }
    return false;
  }
}
```

- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
Tags: [[LeetCode]] - [[Recursion]] - [[Binary Tree]]
