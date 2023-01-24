---
tags: LeetCode
topics: BST
difficulty: hard
performance: uncomplete
date: 2023-01-13 Friday
---
[[Binary Search Tree]]
## Questions

Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return _the **root node reference** (possibly updated) of the BST_.

Basically, the deletion can be divided into two stages:

1.  Search for a node to remove.
2.  If the node is found, delete the node.

## Solution

### Recursion

Time: O(N)
Space: O(N) recursion stack

Takeaways:
- Iterative solution is so difficult - there are so many edge cases to consider, and you have to keep track of the parent too. Maybe it would be easier if parent is a pointer in each node
- When predecessor is found, a neaty recursive tech was used: replace root.val with predecessor.val, then recursively delete the old predecessor from the tree. Edge cases involving the predecessor having children (left child specifically) is handled by deleteNode itself.
- However, copying the value may be problematic. If value is more complicated than an integer, may take more time!

```python
class Solution:

    def predecessor(self, root):
        root = root.left
        while root.right:
            root = root.right
        return root.val        

    def deleteNode(self, root: Optional[TreeNode], key: int) -> Optional[TreeNode]:
        
        if not root:
            return root

        # Recursively serch for the node
        if root.val > key:
            root.left = self.deleteNode(root.left, key)
        elif root.val < key:
            root.right = self.deleteNode(root.right, key)
        else: # found node to be deleted
            # if deleted node is a leaf node, simply delete it
            if not root.left and not root.right:
                root = None
            # if node has one child, replace it with its only child
            elif not root.left or not root.right:
                root = root.left if root.left else root.right
            # if node has both child, replace it with its predeccessor
            else:
                root.val = self.predecessor(root)
                root.left = self.deleteNode(root.left, root.val) # delete the old predecessor, CRUCIAL STEP

        return root
```

### Iterative - O(1) Space

Not my solution though LOL.  Big ideas: 
- To separate handling the root node and handing non-root node, find the deleted node and treat it as the ROOT node to be deleted! BRILLIANT
- Also no value was copied, only swapping is involved, which is harder.

```python
class Solution:

    def predecessor(self, root):
        parent = root
        root = root.left
        while root.right:
            parent = root
            root = root.right
        return parent, root

    # Iteratively delete the root and return the predecessor of root
    def deleteRootNode(self, root):
        if not root: 
            return None
        elif not root.left and not root.right:
            return None
        elif not root.left:
            return root.right
        elif not root.right:
            return root.left
        else: # if root as both left and right children

            parent, predecessor = self.predecessor(root)
            predecessor.right = root.right

            # if predecessor is not root's left child, 
            # take care of predecessor's left child
            if predecessor != root.left: 
                parent.right = predecessor.left
                predecessor.left = root.left
            
            return predecessor



    def deleteNode(self, root: Optional[TreeNode], key: int) -> Optional[TreeNode]:
        if not root:
            return None
        
        parent = None
        curr = root
        while curr and curr.val != key:
            parent = curr
            if curr.val < key:
                curr = curr.right
            else: 
                curr = curr.left
                
        # if root node is to be deleted:
        if not parent:
            return self.deleteRootNode(root)

        # if to-be-deleted node is left child:
        if parent.left == curr:
            parent.left = self.deleteRootNode(curr)
        else:
            parent.right = self.deleteRootNode(curr)

        return root
```