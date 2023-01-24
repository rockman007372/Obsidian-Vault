2022-06-05 16:44
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Binary Tree Level Order Traversal
### Questions
Input: Binary Tree
Output: Nodes ordered by level
`[1, 2, 3, 4, 5 ,6 ,7] -> [[1], [2, 3], [4, 5, 6, 7]]`

### Solution
#### [[Breadth First Search]]
Challenge: Find number of children at each level? 
Solution: no.children = number of elements in the queue in each iteration ([[Loop Invariant]])
Time: O(N)
Space: O(N) - max size of queue

```Java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> levels = new ArrayList<>();
        if (root == null) return levels;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        int level = 0;
        while (!queue.isEmpty()) {
            // start a new level
            levels.add(new ArrayList<>());
            
            // add nodes to the current level
            // number of children in lvel = number of elements in queue
            int levelElements = queue.size();
            for (int i = 0; i < levelElements; i++) {
                TreeNode curr = queue.poll();
                levels.get(level).add(curr.val);
                if (curr.left != null) queue.offer(curr.left);
                if (curr.right != null) queue.offer(curr.right);
            }
            level++;
        }
        
        return levels;
    }
}
```

#### [[Depth First Search]]

```Java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> levels = new ArrayList<>();
        if (root == null) return levels;
        helper(root, levels, 0);
        return levels;
    }
    
    public void helper(TreeNode root, List<List<Integer>> res, int level) {
        if (root == null) return;
        if (res.size() < level + 1) {
            res.add(new ArrayList<>());
        }
        res.get(level).add(root.val);
        helper(root.left, res, level + 1);
        helper(root.right, res, level + 1);
    }
}
```