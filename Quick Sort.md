2022-06-24 00:37
Tags: [[Data Structure and Algorithm]]  - [[Sorting Algorithms]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Quick Sort
### Algorithm
![[Pasted image 20220624003733.png]]

### Implementation
#### Partition algorithm
##### Partition using additional array w/out duplicates
![[Drawing 2022-06-24 01.10.22.excalidraw]]

##### In-place Partition w/out duplicates
![[Quick Sort 2022-06-24 01.14.54.excalidraw]]

Issue with duplicates is that it will cause run-time of Quick Sort to be O($N^2$) if partition algorithm does not take into account duplicates.

Eg: [2, 2, 2, 2, 2] -> each partition will only reduce the search by 1 element -> N passes of O(N) partitions

##### In-place Partion with Duplicates
**Option 1**: two-pass Partitioning
	1. Regular partion (Left side <= piviot)
	2. Pack duplicates (Swap all duplicates to the left of pivot)
![[Quick Sort 2022-06-24 01.33.25.excalidraw]]

**Option 2**: one-pass Partitioning (Maintain 4 regions of array)
![[Drawing 2022-06-24 01.39.04.excalidraw]]

##### Lomuto Partition scheme
- One pointer partition algorithm.
- Easier to implement
- Requires more swaps.
- <mark style="background: #FFB86CA6;">The pivot is at correct position</mark> => recurse on `A[lo, p - 1]` and `A[p + 1, hi]`

```Pseudo
partition(arr[], lo, hi) 
    pivot = arr[hi]
    i = lo     // place for swapping
    for j := lo to hi – 1 do
        if arr[j] <= pivot then
            i = i + 1 
            swap arr[i] with arr[j]
    swap arr[i] with arr[hi]
    return i
```

```Java
static int partition(int[] arr, int low, int high) {
	int pivot = arr[high];
	
	// Index of smaller element
	int i = (low - 1);
	
	for (int j = low; j <= high - 1; j++) {
		// If current element is smaller
		// than or equal to pivot
		if (arr[j] <= pivot) {
			i++; // increment index of
				// smaller element
			Swap(arr, i, j);
		}
	}
	Swap(arr, i + 1, high);
	return (i + 1);
}

static void quickSort(int[] arr, int low, int high) {
	if (low < high)
	{
		/* pi is partitioning index,
		arr[p] is now at right place */
		int pi = partition(arr, low, high);
		
		// Separately sort elements before
		// partition and after partition
		quickSort(arr, low, pi - 1);
		quickSort(arr, pi + 1, high);
	}
}
```

![[Quick Sort 2022-06-24 22.12.48.excalidraw]]

##### Hoarse Partition scheme
+ 2 pointers partition
+ More efficient, fewer swaps
+ Harder to code

![[Pasted image 20220625105435.png]]

```Java
// Java implementation of QuickSort
// using Hoare's partition scheme
import java.io.*;

class GFG {

	/* This function takes first element as pivot, and
	places all the elements smaller than the pivot on the
	left side and all the elements greater than the pivot
	on the right side. It returns the index of the last
	element on the smaller side*/
	static int partition(int[] arr, int low, int high) {
		int pivot = arr[low]; i = low + 1; j = high;
		
		while (true) {
			while (arr[i] < pivot && i < high) i++;
			
			while (arr[j] >= pivot && j > low) j--;
			
			if (j <= i) {
				swap(arr, low, j);
				return j;
			}
			
			swap(arr, i, j);
		}
	}

	/* The main function that
	implements QuickSort
	arr[] --> Array to be sorted,
	low --> Starting index,
	high --> Ending index */
	static void quickSort(int[] arr, int low, int high)
	{
		if (low < high) {
			/* pi is partitioning index,
			arr[p] is now at right place */
			int pi = partition(arr, low, high);

			// Separately sort elements before
			// partition and after partition
			quickSort(arr, low, pi - 1);
			quickSort(arr, pi + 1, high);
		}
	}
}

// This code is contributed by vt_m.

```
### Performance
- Time: 
	- Average: O(NLogN) - T(N) = 2T$(\frac{N}{2})$ + O(N)
	- Worse-Case: O($N^2$) - bad pivot (eg: max, min element as pivot) 
- Space: O(1) since it is in-place
- Stability: Unstable