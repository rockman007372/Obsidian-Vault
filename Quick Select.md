---
tags: algorithm
aliases: 
date: 2022-07-24 Sunday
---

  
Quick select is an algorithm that extends the idea of the [[Quick Sort]] algorithm to efficiently **find the kth smallest (or largest) element in an unsorted list** or array.

#### Algorithm
1. Randomly choose a pivot 
2. Partition around this pivot: O(N)
3. If the position of pivot = k, return pivot. 
	Else, do quicksort on appropriate half

```Java

int partition(int[] arr, int low, int high) {
	int pivot = arr[low]; i = low + 1; j = high;
		
	while (true) {
		while (i <= high && arr[i] < pivot) i++;
			
		while (j > low && arr[j] >= pivot) j--;
			
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
		if (p == k - 1) return A[p];
		else if (p > k - 1) return quickSelect(A, lo, p - 1, k);
		else if (p < k - 1) return quickSelect(A, p + 1, hi, k);
		return -1; // have to return sth
	}
}
```

#### Performance
- Time: O(N)
	T(N) = T($\frac{N}{2}$) + O(N) = O(N);   
- Space: O(1) if in place, depending on partition function.   

#### Question

>[!question]
> Comparing pivot index with k or k - 1?

In Quick select, we typically compare the pivot index with the value `k - 1` (not `k`).

The reason for this is that when we're finding the kth smallest element, we're working with zero-based indexing. So if we want to find the element at index k, it would be the (k+1)th element in one-based indexing. Therefore, we compare the pivot index with `k - 1`.

For example, if we're looking for the 5th smallest element (k = 5), we compare the pivot index with `5 - 1 = 4`. If the pivot index is less than 4, we know that the desired element is in the right partition. If the pivot index is greater than 4, we know that the desired element is in the left partition. And if the pivot index is exactly 4, we have found the 5th smallest element.

This adjustment accounts for the difference between zero-based indexing and one-based indexing and ensures we're comparing the correct indices during the partitioning process in Quick select.
