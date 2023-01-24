2022-06-05 16:44
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# kth Smallest Element in a BST
## My Performance
#complete #notOnTime #notOptimal

## Questions
Input: BST root
Output: $k ^ {th}$ smallest element in BST

## Solution
##### Augmented BST - AVL Ordered Statistic tree
Store the weight of the left child of each node.
Rank = left.weight + 1.

It takes O(N) to update weight. 

If tree is balanced ([[AVL Tree]])
Time: O(lgN) 
Space: O(lgN) 

```Java
class Solution {
    private HashMap<TreeNode, Integer> weightMap = new HashMap<>();
    private boolean updated = false;
    
    public int kthSmallest(TreeNode root, int k) {
        if (!updated) {
            updateWeight(root);
            updated = true;
        }
        
        int rank = weightMap.get(root) + 1;
        
        if (rank == k) return root.val; 
        
        if (rank > k) return kthSmallest(root.left, k);
        
        // if rank < k
        return kthSmallest(root.right, k - rank);
    }
	
	// return the weight of the root node. 
	// Update the node with the weight of its 
	// left child on the way.
    public int updateWeight(TreeNode root) {
        if (root == null) {
            weightMap.put(root, 0);
            return 0;
        }
        
        int leftWeight = updateWeight(root.left);  
        int rightWeight = updateWeight(root.right);
        weightMap.put(root, leftWeight);
        
        return 1 + leftWeight + rightWeight;        
    }
}
```

##### Inorder DFS
The preorder DFS of a BST gives the increasingly-sorted elements in the tree. Then we just have to find the $k^{th} - 1$ element.

Time: O(N)
Space: O(N) to store the sorted nodes

```Java
class Solution {
    public int kthSmallest(TreeNode root, int k) {
        ArrayList<Integer> ordered = inorder(root, new ArrayList<>());
        return ordered.get(k - 1);        
    }
    
    public ArrayList<Integer> inorder(
	    TreeNode node, ArrayList<Integer> res) {
        
        if (node == null) return res;
        
        inorder(node.left, res);
        res.add(node.val);
        inorder(node.right, res);
        
        return res;
    }
}
```

##### Iterative Inorder DFS
Best solution, because we can stop searching after we pop the $k^{th}$ element.

Time: O(N + k), O(N) to reach the leftmost leaf and O(k) to return the kth element (pop k times)

Space: O(N) to keep the stack

```Java
class Solution {
    public int kthSmallest(TreeNode root, int k) {
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            
            // go to left-most leaf node
            while (root != null) {
                stack.push(root);
                root = root.left;
            }
	        
	        // if we pop the kth element, return it
            root = stack.pop();
            if (--k == 0) return root.val;
            
            // add right child to stack and traverse
            root = root.right;
        }
        return -1;
    }
}
```