---
tags: LeetCode
topics: Binary Tree
difficulty: hard
performance: uncomplete
date: 2022-07-24 Sunday
---
[[Binary Tree]]

### Questions
Input: Preorder and Inorder `int[]`
Output: Root of the binary tree 

### Solution
Traverse the preorder array one by one to find the root node, then use inorder array to determine recursively the left and right subtrees.

```Java
class Solution {
    private HashMap<Integer, Integer> inorderMap = new HashMap<>();
    private int[] preorder;
    private int preorderIndex;
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        this.preorder = preorder;
        for (int i = 0; i < inorder.length; i++) {
            inorderMap.put(inorder[i], i);
        }
        return buildHelper(0, inorder.length - 1);
    }   
            
    public TreeNode buildHelper(int inorderLo, int inorderHi) {
        // if (preorderIndex >= preorder.length) return null; // dont even need this condition
        if (inorderLo > inorderHi) return null;
        
        int rootVal = preorder[preorderIndex++];
        TreeNode root = new TreeNode(rootVal);
        
        int pos = inorderMap.get(rootVal);
        root.left = buildHelper(inorderLo, pos - 1);
        root.right = buildHelper(pos + 1, inorderHi);
        
        return root;
    }
}
```

Time: O(N) to traverse
Space: O(N) to store HashMap + recursive stack of O(N) depth


##### Python Solution

Key takeaways:
- Use nonlocal to modify variable in the outer function from within the inner function
- Keep track of indices instead of slicing the whole list

```python
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        
        # build hash map to map inorder value to its index
        inorderIndices = {}
        for i, num in enumerate(inorder):
            inorderIndices[num] = i

        # index to keep track of current root in preorder
        preorderIndex = 0

        def arrayToTree(left, right): # left,right = inorder indices
            
            nonlocal preorderIndex # not local to function

            if left > right: return None # if inorder array is empty, reach leaf node

            # Get current root
            rootVal = preorder[preorderIndex]
            root = TreeNode(rootVal)
            preorderIndex += 1

            leftTree = arrayToTree(left, inorderIndices[rootVal] - 1)
            root.left = leftTree

            rightTree = arrayToTree(inorderIndices[rootVal] + 1, right)
            root.right = rightTree

            return root

        # Recursively call array to tree on each side of the root
        return arrayToTree(0, len(preorder) - 1)
```