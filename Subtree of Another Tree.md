---
tags: LeetCode
topics: binary tree
difficulty: easy
performance: complete, notOnTime, notOptimal
date: 2022-07-24 Sunday
---

## Questions

Given the roots of two binary trees `root` and `subRoot`, return `true` if there is a subtree of `root` with the same structure and node values of `subRoot` and `false` otherwise.

A subtree of a binary tree `tree` is a tree that consists of a node in `tree` and all of this node's descendants. The tree `tree` could also be considered as a subtree of itself. 
![[Pasted image 20220805175045.png]]
## Solution
### Trivial Solution - Topdown comparison
- At every node, check if it is the equal to the subRoot. 
- If it is not, check its children.
- Time: O(S * T) ?
	- S = size of root, T = size of subRoot
	- For each node, we compare it with the subRoot

```Java
class Solution {
    // Time complexity: O(N^2) ?
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if (root == subRoot) return true;
        if (root == null && subRoot == null) return true;
        if (root == null || subRoot == null) return false;
        if (isEqual(root, subRoot)) return true;
        return isSubtree(root.left, subRoot) || isSubtree(root.right, subRoot);
    }
    
    public boolean isEqual(TreeNode s, TreeNode t) {
        if (s == null && t == null) return true;
        if (s == null || t == null) return false;
        if (s.val != t.val) return false;
        return isEqual(s.left, t.left) && isEqual(s.right, t.right);
    }
}
```
Space: O(N) - max recursion stack

### Only compare Trees of the same size
1. Get size of subRoot tree → O(T)
2. Collect all the trees with size t → O(S)
3. Only compare these candidate trees with subtree t → O($\frac{S}{T} * T$) = O(S)
	- Max number of subtrees with size t = $\frac{S}{T}$

Time: O(S + T)
Space: O(S / T)

```Java
class Solution {
    public boolean isSubtree(TreeNode s, TreeNode t) {
        if (s == null && t == null) return true;
        else if ( s == null || t == null) return false;
        
        int m =  collect(t, -1, null); //size of t
        
        List<TreeNode> candidates = new ArrayList<>();
        collect(s, m, candidates); // collect all subtree of size t
        
        for (TreeNode candidate : candidates) {
            if (compare(candidate, t)) return true;
        }
        return false;
    }

    private int collect(TreeNode node, int m, List<TreeNode> candidates) {
        if (node == null) return 0;
        int size =  1 + 
        collect(node.left, m, candidates) + 
        collect(node.right, m, candidates);
        
        if (size == m) { //collect subtree with size of t
            candidates.add(node);
        }
        
        return size;
    }
    
    private boolean compare(TreeNode s, TreeNode t) {
        if (s == null && t == null ) return true;
        else if (s == null || t == null) return false;
        return s.val == t.val 
	        && compare(s.left, t.left) 
	        && compare(s.right, t.right);
    }
}
```

### Serialization and String Matching

Interesting solution making use of preexisiting algorithms:
- Serialise the tree and the subtree similar to [[Serialize and Deserialize Binary Tree]]
- Compare the 2 serialized strings and check if the subtree string is a substring of the tree string ([[Find the Index of the First Occurence in the String]]) 

Time: O(M + N)
- Serialization takes O(M + N)
- Checking substring using KMP algorithm takes O(M + N)

Space: O(M + N)

### Tree Hash

We want to hash (map) each subtree to a unique value. We want to do this in such a way that if two trees are identical, then their hash values are equal. And, if two trees are not identical, then their hash values are not equal. This hashing can be used to compare two trees in O(1) time.

We will build the hash of each node depending on the hash of its left and right child. The hash of the `root` node will represent the hash of the whole tree because to build the hash of the `root` node, we used (directly, or indirectly) the hash values of all the nodes in its subtree.

There can be multiple ways of hashing the tree. We want to use that mechanism which is
-   Simple to calculate
-   Efficient
-   Has minimum spurious hits

> **Spurious Hits:** If hash values of two trees are equal, and still they are not identical, then we call it a spurious hit. A spurious hit is a case of False Positive.

We will use the following hashing function.

-   If it's a `null` node, then hash it to `3`. (We can use any prime number here)
-   Else,
    -   left shift the hash value of the left node by some fixed value.
    -   left shift hash value of right node by 1
    -   add these shifted values with this `node->val` to get the hash of this node.

Please note that one should avoid concatenating strings for hash value purposes because it will take O(N) time to concatenate strings.

To ensure minimum spurious hits, we can map each node to two hash values, thus getting one hash pair for each node. Trees rooted at `s` and Tree rooted at `t` will have the same hash pair **iff** they are identical, provided our hashing technique maps nodes to unique hash pairs.

Time: O(M + N)
- O(M + N) to hash both trees
- O(M + N) to compare each subtree, since each comparison takes O(1) with hashing
