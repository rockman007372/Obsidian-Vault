---
tags: 
aliases: 
date: 2022-07-24 Sunday
---
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
### Algorithm

Quick sort is an efficient sorting algorithm that follows the **divide-and-conquer** approach and is based on the principle of **partitioning**.

Algorithm:
1.  Choose a pivot element from the list. 
2.  **Partition** the list by rearranging its elements such that all elements smaller than the pivot are placed before it, and all elements greater than the pivot are placed after it. The pivot is now in its sorted position.
3.  Repeat the above steps recursively on the sublists formed by the partition until the entire list is sorted.
4.  The base case of the recursion is when a sublist has zero or one element, in which case it is already considered sorted.

![[Pasted image 20220624003733.png]]

### Implementation

The partitioning step is a crucial part of the Quick sort algorithm. There are 2 common approaches to determine the position of the pivot element in the sorted list:

- [[Lomuto Partition Scheme]]
- [[Hoarse Partition Scheme]]

See more at [[Partition Algorithms]]

### Performance

Time: 
- Average: O(NLogN) 
	- T(N) = 2T$(\frac{N}{2})$ + O(N)
- Worse-Case: O($N^2$) 
	- Every random pivot is a bad pivot (eg: max, min element as pivot) 

Space: O(1) since it is in-place

Stability: Unstable