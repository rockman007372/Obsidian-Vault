2022-06-06 20:05
Tags: [[Data Structure and Algorithm]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

## Template 1

Most common and straightforward template:

```python
def binarySearch(nums, target):
    """
    :type nums: List[int]
    :type target: int
    :rtype: int
    """
    if len(nums) == 0:
        return -1

    left, right = 0, len(nums) - 1
    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    # End Condition: left > right
    return -1
```

**Syntax:**
-   Initial Condition: `left = 0, right = length-1`
-   Termination: `left > right`
-   Searching Left: `right = mid-1`
-   Searching Right: `left = mid+1`

**Key attributes:**
-   Search Condition can be determined without comparing to the element's neighbors (or use specific elements around it)
-   No post-processing required because at each step, you are checking to see if the element has been found. If you reach the end, then you know the element is not found

## Template 2 (CS2040S)

### Search

```Java
public int binarySearch(int[] nums, target) {
	int lo = 0;
	int hi = nums.length - 1;
	while (lo < hi) {
		int mid = lo + (hi - lo) / 2;
		if (nums[mid] >= target) {
			hi = mid; // mid could be the answer
		} else {
			lo = mid + 1;
		}
	}
	return nums[lo] == target ? lo : -1;
}
```

**Syntax:**
-   Initial Condition: `left = 0, right = length - 1`
-   Termination: `left == right` (when there is only 1 element left)
-   Searching Left: `right = mid`
-   Searching Right: `left = mid + 1`

**Key attributes:**
-   Guarantees Search Space is at least 2 in size at each step
-   Post-processing required. Loop/Recursion ends when you have 1 element left. Need to assess if the remaining element meets the condition.

### Generalised

You can generalise Template 2 to any binary search problem with a condition:

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

**Example:** Find minimum number of features n such that explained variance is at least 99%:

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

## Template 3

```python
def binarySearch(nums, target):
    """
    :type nums: List[int]
    :type target: int
    :rtype: int
    """
    if len(nums) == 0:
        return -1

    left, right = 0, len(nums) - 1
    while left + 1 < right:
        mid = (left + right) // 2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid
        else:
            right = mid

    # Post-processing:
    # End Condition: left + 1 == right
    if nums[left] == target: return left
    if nums[right] == target: return right
    return -1
```

**Syntax:**
-   Initial Condition: `left = 0, right = length - 1`
-   Termination: `left + 1 == right` (when there are 2 elements left)
-   Searching Left: `right = mid`
-   Searching Right: `left = mid`

**Key attributes:**
-   Gurantees Search Space is at least 3 in size at each step
-   Post-processing required. Loop/Recursion ends when you have 2 elements left. Need to assess if the remaining elements meet the condition.