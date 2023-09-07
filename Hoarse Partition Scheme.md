+ 2 pointers partition
+ More efficient, fewer swaps
+ Harder to code

![[Pasted image 20220625105435.png]]

```Java
// Java implementation of QuickSort
// using Hoare's partition scheme
import java.io.*;

class GFG {

	/* Partitions and returns the index of the last
	element on the smaller side*/
	static int partition(int[] arr, int low, int high) {
		int pivot = arr[low]; // take first elem as pivot
		int i = low + 1; 
		int j = high;
		
		while (true) {
			// Increments i until reaching an element >= pivot
			while (i < high && arr[i] < pivot ) {
				i++;
			}
			
			// Increments i until reaching an element < pivot
			while (j > low && arr[j] >= pivot) {
				j--;
			}
			
			// Once 2 pointers meet, swap pivot with element at j
			if (j <= i) {
				swap(arr, low, j);
				return j;
			}
			
			// Else, swap i and j as normal
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
```