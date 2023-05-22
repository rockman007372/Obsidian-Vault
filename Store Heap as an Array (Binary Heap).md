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
  

[[How to build a binary heap (Heapify)]]
[[Heap Sort]]