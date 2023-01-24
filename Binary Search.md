2022-06-06 20:05
Tags: [[Data Structure and Algorithm]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
### Template

```Java
public int binarySearch(int[] nums, target) {
	int lo = 0;
	int hi = nums.length - 1;
	while (lo < hi) {
		int mid = lo + (hi - lo) / 2;
		if (nums[mid] >= target) {
			hi = mid;
		} else {
			lo = mid + 1;
		}
	}
	return nums[lo] == target ? lo : -1;
}
```

```Python
def binary_search(array) -> int:
    def condition(value) -> bool:
        pass
        
    # could be [0, n], [1, n] etc. Depends on problem
    left, right = min(search_space), max(search_space) 
    
    while left < right:
        mid = left + (right - left) // 2
        if condition(mid):
            right = mid
        else:
            left = mid + 1
    return left # could be left or left - 1 (left is the minimum to satisfy the condition)
```

Steps to modify the template: 
1. Initialize boundary condition correctly (left and right). Must include all possible elements to return
2. Decide return values (`left` or `left - 1`); *left* is the minimum value to satisfy the condition
3. Design condition

## Example code:

Find minimum number of features n such that explained variance is at least 99%:

```python
def variance_retained(s, k):
    return (np.sum(s[:k]) / np.sum(s)) >= 0.99

def binary_search(pca):
    max = 784
    min = 0

    while min < max:
        mid = min + (max - min) // 2
        retain = variance_retained(pca.singular_values_, mid)
        
        if retain:
            max = mid  # if condition true, ans could be mid or less than mid
        else:
            min = mid + 1 # if condition is false, ans could NOT be mid
            
    return min

binary_search(full_pca)
```