2022-06-05 16:44
Tags: [[LeetCode]] - [[Binary Search Tree]] - [[Depth First Search]] - [[Breadth First Search]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Validate Binary Search Tree
### Questions
Input: Root of BST
Output: Boolean value determining if it is a valid BST

### Solution
##### Recursion with valid range
We cannot just compare left child and right child with root at every stage. We must keep a low and hi range and compare the current node to that range.

```Java
class Solution {
    public boolean validate(TreeNode root, Integer low, Integer high) {
        // Empty trees are valid BSTs.
        if (root == null) {
            return true;
        }
        // The current node's value must be between low and high. 
        // -> Instead of check true condition, check false condition to reduce logic
        if ((low != null && root.val <= low) || (high != null && root.val >= high)) {
            return false; 
        }
        // The left and right subtree must also be valid.
        return validate(root.right, root.val, high) && validate(root.left, low, root.val);
    }

    public boolean isValidBST(TreeNode root) {
        return validate(root, null, null);
    }
}

```

Time: O(N) to search entire tree
Space: O(h) recursion deep = O(N)

##### Iterative DFS using Stack

```Java
class Solution {
	// Stack FIFO, keep 3 stacks to track the current node and its current range
    private Deque<TreeNode> stack = new LinkedList();
    private Deque<Integer> upperLimits = new LinkedList();
    private Deque<Integer> lowerLimits = new LinkedList();

    public void update(TreeNode root, Integer low, Integer high) {
        stack.add(root);
        lowerLimits.add(low);
        upperLimits.add(high);
    }

    public boolean isValidBST(TreeNode root) {
        Integer low = null, high = null, val;
        update(root, low, high);

        while (!stack.isEmpty()) {
            root = stack.poll();
            low = lowerLimits.poll();
            high = upperLimits.poll();

            if (root == null) continue;
            val = root.val;
            if (low != null && val <= low) {
                return false;
            }
            if (high != null && val >= high) {
                return false;
            }
            update(root.right, val, high);
            update(root.left, low, val);
        }
        return true;
    }
}
```

###### Why is BFS potentially slower than DFS? 
Since there is no logical relation between two elements at same level, there is higher probability that we may have to traverse more level before confirming in BFS. However, with DFS, we eliminate the validity at the branch level and return early in case tree is invalid.

##### Inorder DFS
By the nature of Inorder DFS, if consecutive elements are out of order, it is not a valid DFS.

![[Pasted image 20220622144952.png]]

```Java
class Solution {
	private Integer prev; // Integer, not int, because Integer is initialized as null
	public boolean isValidBST(TreeNode root) {
		return inorder(root);
	}
	
	public boolean inorder(TreeNode root) {
		if (root == null) return true;
		if (!inorder(root.left)) {
			return false;
		}
		
		if (prev != null && prev >= root.val) {
			return false;
		}
		
		prev = root.val;
		return inorder(root.right);
	}
}
```