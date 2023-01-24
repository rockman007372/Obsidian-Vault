---
tags: data structure
aliases: 
date: 2022-07-24 Sunday
---

## Definition

![[Pasted image 20230112120116.png]]


## 3 Facts to Know about BST

1.  Inorder traversal of BST is an array sorted in the ascending order.
2. Successor = "after node", i.e. the next node, or the smallest node _after_ the current one.
	- To find a successor, go to the right once and then as many times to the left as you could.
3. Predecessor = "before node", i.e. the previous node, or the largest node _before_ the current one.
	- To find a predecessor, go to the left once and then as many times to the right as you could.

![[Pasted image 20230112125811.png]]


## BTS Heights

Number of edges on the longest path from root to tree

```
h(v) = 0
h(v) = max(h(v.left), h(v.right)) + 1
h(null) = -1
```

## Balanced Search Trees

Operations in Binary Tree takes O(h) time:$$log(n) - 1 \leq h \leq n$$
> [!definition]
> A BST is balanced if h = O(log n)

h = O(N) if tree is unbalanced.
h = O(lgN) if tree is balanced. 

**How to get a balanced tree?**
- Define a good property of the a tree
- Show that if the good property holds then the tree is balanced
- After every insert / delete, make sure the good property still holds. Else, fix it (Invariant)


## AVL Tree

AVL tree is a form of balanced binary tree.

**Augment:** 
- Every node v stores height attribute. `v.height = h(v)`
- On insert and delete, update height

**Balance Invariant:**

![[Pasted image 20230112121522.png]]
- A node is height-balanced if $|v.left.height - v.right.height| \leq 1$. 
- In other words, left child and right child's height must not be different by more than 1
- An AVL tree is height-balanced if every node in tree is height-balanced

>[!Theorem]
> A height-balanced tree with n nodes has at most height $h < 2log(n)$.
> Hence a height-balanced tree is also a balanced tree since $h = O(log(n))$.

**Proof:**

$h < 2log(n) ⇒ \frac{h}{2} < log(n) ⇒ 2^{\frac{h}{2}} < n$

Hence we have to prove a tree with height h has at least $n > 2^{h/2}$ nodes.
$$
\begin{align*}
n_{h} &= 1 + n_{h-1} + n_{h-2}\\
& \geq 2 * n_{h-2}\\
& \geq 4 * n_{h - 4}\\
& \geq 8 * n_{h - 6}\\
& \geq ...\\
& \geq 2^{\frac{h}{2}} * n_{0}, \text{ where } n_{0} = 1 
\end{align*}
$$
Key idea is we skip every other level, hence k = h/2.


## Key Operations

Modifying operations: O(h)
- Insert (see [[Insert Into a Binary Search Tree]])
- Delete

Query Operations: O(h)
- Search
- Predecessor, Sucessor
- findMax, findMin





---
Links: 
