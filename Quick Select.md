2022-06-23 18:06
Tags: {{[[Data Structure and Algorithm]]}}  
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Quick Select
### Main Points
Idea is very similar to [[Quick Sort]].
Allows us to find the $k^{th}$ ranked elements.  

#### Algorithm
1. Randomly choose a pivot 
2. Partition around this pivot: O(N)
3. If the position of pivot = k, return pivot. 
	Else, do quicksort on appropriate half

```Java

int partition(int[] arr, int low, int high) {
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

int quickSelect(array A, lo, hi, k) {
	if (lo == hi) return A[lo]; // array length = 1
	else {
		pIndex = Math.random(lo, hi);
		p = partition(A, lo, hi, pIndex); // pivot index after partition 
		if (k == p + 1) return A[p];
		else if (k < p + 1) return quickSelect(A, lo, p - 1, k);
		else if (k > p + 1) return quickSelect(A, p + 1, hi, k);
		return -1; // have to return sth
	}
}
```

#### Performance
- Time: O(N)
	T(N) = T($\frac{N}{2}$) + O(N) = O(N);   
- Space: O(1) if in place, depending on partition function.   
