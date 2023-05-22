Use an array of n cells to store n nodes in the heap.

Store the heap in BFS order: 

![[Heap 2022-06-23 14.17.11.excalidraw|400 x 400]]


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
+ parent of node u =  `A[(j - 1) // 2]`