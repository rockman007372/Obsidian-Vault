2022-06-23 01:24
Tags: [[Heap]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

### Main Points
A sorting algorithm based on [[Heap]].

#### Algorithm

![[Pasted image 20230109221008.png]]

1. Heapify array : O(N) 
2. Swap first element (root / max element) with last element (rightmost child), reduce heap size by one, bubble down the new first element: O(logN)
3. Repeat N - 1 times to sort.

HeapSort is a superior version of [[Selection Sort]].

#### Performance
- Time: O($N * lgN$)
- Space: O(1) - the heap is formed using input array! No additional space.
- In-Place sorting.
- Stability: unstable (cannot handle duplicate)