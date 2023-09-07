## Abstract implementations

### Additional array 

Iterate through all the elements in the original array. If the current element is less than the pivot element, append it to the position `lo` in the additional arrray, then increment the lo pointer. Do the same for the `hi` pointer, but decrement it. Repeat until `lo` == `hi`.

![[Drawing 2022-06-24 01.10.22.excalidraw]]

### In-place Partition without duplicates

![[Quick Sort 2022-06-24 01.14.54.excalidraw]]

Issue with duplicates is that it will cause run-time of Quick Sort to be O($N^2$).

Eg: [2, 2, 2, 2, 2] -> each partition will only reduce the search by 1 element -> N passes of O(N) partitions

### In-place Partion with Duplicates

**Option 1**: two-pass Partitioning
	1. Regular partion (Left side <= piviot)
	2. Pack duplicates (Swap all duplicates to the left of pivot)
	3. Recurse on 2 sides, but ignore the duplicates in the middle.

![[Quick Sort 2022-06-24 01.33.25.excalidraw]]

**Option 2**: one-pass Partitioning (Maintain 4 regions of array)

![[Drawing 2022-06-24 01.39.04.excalidraw]]

## Concrete Implementations

[[Lomuto Partition Scheme]]

[[Hoarse Partition Scheme]]