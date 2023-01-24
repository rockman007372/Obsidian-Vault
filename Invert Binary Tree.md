 2022-06-05 16:44
Tags: [[LeetCode]] - [[Binary Tree]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Invert Binary Tree
### Questions
Input: Root of BT
Output: Return the root of the inverted BT

### Solution

##### Recursion

```Java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) {
            return root;
        }
        
        // 1. Invert left and right child subtree
        root.left = invertTree(root.left);
        root.right = invertTree(root.right);
        
        // 2. Switch left and right child
        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;
        
        // 3. Return root
        return root;
    }
}
```

Time: O(N)
Space: O(h) = O(N), tree is not balanced

##### Iterative

Similar to [[Breadth First Search]]

```Javaclass Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        LinkedList<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            TreeNode node = queue.remove();
            TreeNode temp = node.left;
            node.left = node.right;
            node.right = temp;
            if (node.left != null) queue.add(node.left);
            if (node.right != null) queue.add(node.right);
        }
        return root;
    }
}
```

Time: O(N)

Space: O(N) 
At worst case the queue holds all the nodes in one level. 
In a Full Binary Tree, number of leaves = $\frac{(N + 1) }{2}$ = O(N) - [[Full Binary Tree Theorem]] 