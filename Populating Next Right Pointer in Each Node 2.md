---
tags: LeetCode
topics: binary tree, BFS
difficulty: medium
performance: complete
date: 2023-01-16 Monday
---

## Questions

Given a binary tree

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/02/15/117_sample.png)

**Input:** root = `[1,2,3,4,5,null,7]`
**Output:** `[1,#,2,3,#,4,5,7,#]`
**Explanation:** Given the above binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.

**Example 2:**

**Input:** root = `[]`
**Output:** `[]`

## Solution

### BFS

At each frontier in BFS, connect them all.

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val: int = 0, left: 'Node' = None, right: 'Node' = None, next: 'Node' = None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""

class Solution:
    def connect(self, root: 'Node') -> 'Node':

        if not root:
            return root

        # BFS using a queue
        frontier = [root]

        while frontier:
            next_frontier = []

            for node in frontier:
                if node.left:
                    next_frontier.append(node.left)
                if node.right:
                    next_frontier.append(node.right)
            
            # After adding next frontier into queue, link them all
            for i in range(len(frontier)):
                if i == len(frontier) - 1:
                    frontier[i].next = None
                else:
                    frontier[i].next = frontier[i + 1]

            frontier = next_frontier

        return root
```

**Complexity Analysis**

- Time Complexity: O(N) since we process each node exactly once. Note that processing a node in this context means popping the node from the queue and then establishing the next pointers.
- Space Complexity: O(N). This is a perfect binary tree which means the last level contains N/2 nodes. The space complexity for breadth first traversal is the maximum space occupied and the space occupied by the queue is dependent upon the maximum number of nodes in particular level. So, in this case, the space complexity would be O(N).

### Constant Space Solution


Big idea: 
- Instead of using a queue, we can keep track of the current layer using the next pointer (seeing the current layer as a linked list)
- As we traverse the linked list in the current layer, we add the next links to the next layers at the same time.
- We need 3 pointers / variables to keep track of:
	- `curr` points to the current node in the current layer
	- `prev` points to the current node in the next layer (that we want to add the next link to)
	- `leftmost` points to the head of the linked list of the next layer

```python
class Solution:
    def connect(self, root: 'Node') -> 'Node':

        if not root:
            return root

        def process(nextNode: 'Node', currNode, leftmost):
            """
            1. Identify if the head (leftmost) of the next layer if necessary
            2. Set up the links in the next layer.
            3. Increment nextCurr pointer.
            """

            if nextNode:
                if not currNode: # first time reaching this node
                    leftmost = nextNode # set it as head of linked list
                else:
                    currNode.next = nextNode # else add the next link 
                
                currNode = nextNode # either way, increment pointer

            return currNode, leftmost
        

        leftmost = root # head of the next linked list (in the next layer)
        while leftmost:
            curr, prev = leftmost, None # pointers to the current and next layer

            # why? to quite loop in case there is no more leftmost node
            leftmost = None

            # traverse the current layer (should already be a linked list → invariant)
            while curr: 

                prev, leftmost = process(curr.left, prev, leftmost)
                prev, leftmost = process(curr.right, prev, leftmost)

                curr = curr.next

        return root
```