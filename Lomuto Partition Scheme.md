
- One pointer partition algorithm.
- Easier to implement
- Requires more swaps.
- The pivot is at correct position => recurse on `A[lo, p - 1]` and `A[p + 1, hi]`

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

![[Quick Sort 2022-06-24 22.12.48.excalidraw|700]]