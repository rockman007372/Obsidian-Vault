2022-06-05 16:44
Tags: [[LeetCode]] - [[Binary Search Tree]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
### My Performance

### Questions
Input: root of BST, node p, node q
Output: lowest common ancestor

### Solution
Make use of BST property.

##### Recursive 
```Java
class Solution {
    // Binary Search Tree Property!!
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        int rootVal = root.val;
        int pVal = p.val;
        int qVal = q.val;
        
        // if p.val, q.val < root.val, recurse left
        if (pVal < rootVal && qVal < rootVal) 
            return lowestCommonAncestor(root.left, p, q);
     
        // else if p.val, q.val > root.val, recurse right
        if (pVal > rootVal && qVal > rootVal) 
            return lowestCommonAncestor(root.right, p, q);
        
        // else, either lowest ancesstor is in between p and q 
        // or one of p or q  
        return root;
    }
}
```

Time: O(N) - skewed tree, worse case we have to visit all the nodes
Space: O(N) - height if O(N) for skewed tree

##### Iterative
This question is iterative in nature, we just need to find the split node!
```Java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {

        // Value of p
        int pVal = p.val;

        // Value of q;
        int qVal = q.val;

        // Start from the root node of the tree
        TreeNode node = root;

        // Traverse the tree
        while (node != null) {

            // Value of ancestor/parent node.
            int parentVal = node.val;

            if (pVal > parentVal && qVal > parentVal) {
                // If both p and q are greater than parent
                node = node.right;
            } else if (pVal < parentVal && qVal < parentVal) {
                // If both p and q are lesser than parent
                node = node.left;
            } else {
                // We have found the split point, i.e. the LCA node.
                return node;
            }
        }
        return null;
    }
}
```

Time: O(N) - skewed tree, worse case we have to visit all the nodes
Space: O(1)