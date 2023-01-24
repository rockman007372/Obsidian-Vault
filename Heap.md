2022-06-23 01:25
Tags: [[Data Structure and Algorithm]]  - [[Priority Queue]]
- - - 

### Definition
Heap is an implementation of [[Priority Queue]]. It supports the following operations:

| Operation                   | Behavior                                            | Time    |
| --------------------------- | --------------------------------------------------- | ------- |
| insert(Priority, name)      | Inserts an item with the specific name and priority | O(logn) |
| extractMax()                | Extract item with largest priority and delete it    | O(logn) |
| decreaseKey(priority, name) | Reduce the item with that name to a lower priority  | O(logn) |
| increaseKey(priority, name) | Same idea but increase priority                     | O(logn) |
| remove(name)                | remove key from heap                                | O(logn) |
| heapify(array)              | create a heap out of a given array                  | O(n)    | 

Can be used to sort for `O(NlgN)` (see [[Heap Sort]] )

#### Properties
A heap is a binary tree, where the keys are priority. It maintains 2 properties:
1. Max Heap Property: The key of every node is greater than the key of its children.
2. Complete Tree: Every level of the tree must be full except possibly the leaves. Leaf nodes are as far left as possible.

	![[Heap 2022-06-23 13.47.33.excalidraw]]

Max height of a Heap = $\lfloor log(n) \rfloor$ (full binary tree except for leaves level, hence round down)

### Key operations: Bubble Up/Down

![[Heap 2022-06-23 14.17.11.excalidraw]]
##### 1. bubbleUp
Compare the priority of a node to its parent, then swap them if they are misordered. Continue walking the same node up the tree until it is in the correct position.

```pseudo code
bubbleUp(Node u) 
	while u is not the root
		if (u.priority > u.parent.priority) 
			swap(u, u.parent)
		u = parent(u)
```

Do we care if the parent node is misordered as well? 
⇒ IMPOSSIBLE, due to Max Heap Property, the parent must already be greater that its children, and by extension, its grandchildren.

##### 2. bubbleDown
  Compare priority of a node to its children, then swap if they are misordered. Walk down the tree until node is in correct position.

```pseudo
bubbleDown(Node u)
	while u is not a leaf:
		maxP = max(u.left.priority, u.right.priority) 
		// ensure we swap down the with larger child 
		// to maintain maxHeap property 
		
		if (maxP > u.priority) {
			// if 2 priority are equal, swap with left child first
			if (maxP == u.left.priority)
				swap(u, u.left)
				u = u.left
			else if (maxP == u.right.priority)
				swap(u, u.right)
				u = u.right
		}
```


- Each tries to move the node up or down until it satisfies the MaxHeap Property. 
- Using these operations, we can implement `increaseKey/decreaseKey`

### Implementation of PQ operations
##### 1. increaseKey
Find the key then bubbleUp the key. 
O(lgN) to traverse up.

##### 2. decreaseKey
bubbleDown the key with its GREATER child (to maintain MaxHeap Property). Else, if we do otherwise:

![[Heap 2022-06-23 14.23.26.excalidraw]]

##### 3. insert
1. Add the new node to the *next insertion spot* (left-most available spot) to maintain Complete Tree property. 
2. Bubble up the new node. 

eg: insert(25)
![[Pasted image 20220623142748.png]]

##### 4. extractMax
Swap with the *right-most* leaf node at the lowest level, then bubble down with the *greater child*.
![[Heap 2022-06-23 14.32.05.excalidraw]]

### Store Heap as an Array (Binary Heap)
Use an array of n cells to store n nodes in the heap.

Store the heap in BFS order: 

```
  left   right
	 v	 v	
[28, 9, 22, 5, 3, 15, 7, 1, 4] - from the example
 ^ 
 root
```

If node u is stored in `A[j]`, we can find:
+ left child of node u = `A[j * 2 + 1]`
+ right child of node u = `A[j * 2 + 2]`
+ parent of node u =  `A[Math.floor( (j - 1) / 2 )]`
  
### Building a heap (Heapify)
Given an array of priorities in a random order, we can heapify using this algorithm: 

```Java
Heapify(int[] priorities) {
	// Starting at the end, perform bubble down on each element (right to left)
	for (int i = priority.length - 1; i >= 0; i--) {
		bubbleDown(i);
	}
	// Can do better: starting at last non-leaf node (index = n / 2 - 1)
	// eg: [3, 2, 4, 5, 6, 1]
	//            ^ start here
}
```

Using abstract math, we can prove Heapify has asymptotic cost of O(N) .

### Heap Sort

![[Heap Sort]]