---
tags: 
aliases: Binary Heap
date: 2022-07-24 Sunday
---
![[Pasted image 20220623150048.png]]

Heap is an efficient **implementation** of [[Priority Queue]]. It supports the following operations:

| Operation                   | Behavior                                            | Time    |
| --------------------------- | --------------------------------------------------- | ------- |
| insert(priority, name)      | Inserts an item with the specific name and priority | O(logn) |
| extractMax()                | Extract item with largest priority and delete it    | O(logn) or O(1) |
| decreaseKey(priority, name) | Reduce the item with that name to a lower priority  | O(logn) |
| increaseKey(priority, name) | Same idea but increase priority                     | O(logn) |
| remove(name)                | remove key from heap                                | O(logn) |
| heapify(array)              | create a heap out of a given array                  | O(n)    | 


## Properties

A heap is a binary tree, where the keys are priority. It maintains 2 properties:

1. **Max Heap Property**: The key of every node is greater than the key of its children.
2. **Complete Tree**: Every level of the tree must be full except possibly the leaves. Leaf nodes are as far left as possible.

	![[Heap 2022-06-23 13.47.33.excalidraw]]

Max height of a Heap = $\lfloor log(n) \rfloor$ (full binary tree except for leaves level, hence round down)

---
See also:
- [[Implementation of Heap operations]]
- [[Heap as an Array]]
- [[How to build a binary heap (Heapify)]]
- [[Heap Sort]]





