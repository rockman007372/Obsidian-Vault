Given a array S, count the number of inversions. An inversion is a pair of number `S[i]` and `S[j]` such that:
- `i < j`
- `S[i] > S[j]`

Algorithm:

```python
Sort-and-Count(L) { 
	if list L has one element 
		return 0 and the list L 
	
	Divide the list into two halves A and B 
	(rA, A) = Sort-and-Count(A) 
	(rB, B) = Sort-and-Count(B) 
	(r, L) = Merge-and-Count(A, B) 
	return r = rA + rB + r and the sorted list L 
}

# Merge-and-Count: 
# count the number of inversions between the 2 lists in O(N) time, 
# then merge them normally like Merge Sort.
```

Time: O(NlgN)
Space: O(1) if sorted in place, else O(N) or O(NlgN)

Concrete implementation: [[Reversed Pair]]