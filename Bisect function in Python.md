The purpose of the Bisect algorithm is to find a position in the list where a data element must be inserted to **keep the list sorted.**

The `bisect()` and `bisect_right()` function behave similarly: if the data element is already present in the list, the rightmost position where the data element must be included is returned.

For `bisect_left()`, if the data element is already present in the list, the leftmost position where the data element needs to be included is returned.

```python
						 bisect/bisect_right
						 v
arr = [1, 2, 3, 3, 3, 3, 6, 7, 8, 9]
			 ^
			 bisect_left
 
idx = bisect.bisect(arr, 3)       # gives 6
idx = bisect.bisect_right(arr, 3) # gives 6
idx = bisect.bisect_left(arr, 3)  # gives 2
```

Hence, we should use `bisect_left` to implement binary search.


