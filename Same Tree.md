2022-06-05 16:44
Tags: [[LeetCode]] - [[Depth First Search]] - [[Breadth First Search]] - [[Binary Tree]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Same Tree
### Questions
Input: Roots of 2 binary tree
Output: Boolean whether 2 trees are identical structurally 

### Solution
#### Recursive DFS
Remember to check base case first!

```Java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        // base cases 
		if (p == null && q == null) return true;
		if (p == null || q == null) return false;
		if (p.val != q.val) return false;

		return isSameTree(p.left, q.left) && 
               isSameTree(p.right, q.right);  
    }
}
```
Time: O(N) - Space: O(N)

#### Iterative DFS
Use a Stack/Deque
Time: O(N)
Space: O(N) because size of stack is at most height of tree

```Java
class Solution {
  public boolean check(TreeNode p, TreeNode q) {
    // p and q are null
    if (p == null && q == null) return true;
    // one of p and q is null
    if (q == null || p == null) return false;
    if (p.val != q.val) return false;
    return true;
  }

  public boolean isSameTree(TreeNode p, TreeNode q) {
    if (p == null && q == null) return true;
    if (!check(p, q)) return false;

    // init deques
    ArrayDeque<TreeNode> deqP = new ArrayDeque<TreeNode>();
    ArrayDeque<TreeNode> deqQ = new ArrayDeque<TreeNode>();
    deqP.addLast(p);
    deqQ.addLast(q);

    while (!deqP.isEmpty()) {
      p = deqP.removeFirst();
      q = deqQ.removeFirst();

      if (!check(p, q)) return false;
      if (p != null) {
        // in Java nulls are not allowed in Deque
        if (!check(p.left, q.left)) return false;
        if (p.left != null) { // if p.left != null, q.left != null also if we reach here
          deqP.addLast(p.left);
          deqQ.addLast(q.left);
        }
        
        if (!check(p.right, q.right)) return false;
        if (p.right != null) {
          deqP.addLast(p.right);
          deqQ.addLast(q.right);
        }
      }
    }
    return true;
  }
}
```

```python
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        stack1 = []
        stack2 = []

        stack1.append(p)
        stack2.append(q)

        while stack1 and stack2:
            curr1 = stack1.pop()
            curr2 = stack2.pop()

            if not curr1 and not curr2:
                continue
            elif not curr1 or not curr2:
                return False
            elif curr1.val != curr2.val:
                return False
            else:
	            # In Python None are allowed in list
                stack1.append(curr1.right)
                stack1.append(curr1.left)
                stack2.append(curr2.right)
                stack2.append(curr2.left)
        
        return True
```

#### Iterative BFS
Use a Queue
Time: O(N)
Space: O(N) - max size of queue = numbers of leaves = O(N) 

```
-> [root] ->
-> [right, left] ->
-> [left.child2, left.child1, right] ->
-> [right.child2, right.child1, left.child2, left.child1] ->
```

```Java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        Queue<TreeNode> queue = new LinkedList<>();
        if (p == null && q == null) return true;
        if (p == null || q == null) return false;
        queue.offer(p);
        queue.offer(q);
        
        while (!queue.isEmpty()) {
            TreeNode first = queue.poll();
            TreeNode second = queue.poll();
            if (first == null && second == null)
                continue; // tree not necessarily the same
            if (first == null || second == null)
                return false;
            if (first.val != second.val)
                return false;
            queue.offer(first.left);
            queue.offer(second.left);
            queue.offer(first.right);
            queue.offer(second.right);
        }
        return true;
    }
}
```
