
## Bubble up / down

These operations move the node up and down until the heap satisfies the Max Heap Property. They are the basic operation used to implements other heap's operations.

### bubbleUp

Compare the priority of a node to its parent, then swap them if they are misordered. Continue walking the same node up the tree until it is in the correct position.

```pseudo code
bubbleUp(Node u) 
	while u is not the root
		if (u.priority > u.parent.priority) 
			swap(u, u.parent)
		u = parent(u)
```

>[!question]
> Q: Do we care if the parent node is misordered after being bubbled down? 
> A: IMPOSSIBLE, due to Max Heap Property, the parent must already be greater that its children, and by extension, its grandchildren.

### bubbleDown

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

Its important to swap the node with its **greater** child to maintain MaxHeap Property. Else, if we do otherwise:

![[Heap 2022-06-23 14.23.26.excalidraw]]

## Heap operations

### increaseKey

1. Find the key and adjust priority (would this take O(N) time?)
2. bubbleUp the key with the new priority. 

### decreaseKey

1. Find the key and adjust priority 
2. bubbleDown the key. 

### insert

1. Add the new node to the *next insertion spot* to maintain Complete Tree property. 
2. Bubble up the new node. 

Example: insert(25)

![[Pasted image 20220623142748.png]]

### extractMax

1. Swap with the *right-most* leaf node with the max node.
2. Bubble down the leaf node (with the *greater child*).
3. Return the max node

![[Heap 2022-06-23 14.32.05.excalidraw]]


  
