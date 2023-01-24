---
tags: LeetCode
topics: binary_search
difficulty: medium
performance: uncomplete
date: 2022-10-30 Sunday
---

### Questions

Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value.

If target is not found in the array, return `[-1, -1]`.

You must write an algorithm with O(log n) runtime complexity.

### Solution

- Bad idea: Do binary search for the first position and search linearly for the last position → O(N) worst case
- Solution: do binary search twice, one for the first and one for the last position

```python
class Solution:
    def searchRange(self, nums, target):
        if len(nums) == 0:
            return [-1, -1]
        
        def search(nums, target, left):
            lo = 0
            hi = len(nums) - 1
            
            if left:
                while lo < hi:
                    mid = lo + (hi - lo) // 2
                    
                    if (nums[mid] == target):
	                    # We check if its first element, and recurse accordingly
                        if mid == lo or nums[mid - 1] != target:
                            return mid
                        else:
                            hi = mid - 1
                    
                    elif (nums[mid] > target):
                        hi = mid - 1
                    
                    else:
                        lo = mid + 1
                
                if nums[lo] == target:
                    return lo
                else:
                    return -1
            
            else:
                
                # [1, 2, 3, 4, 4, 10]
                
                while lo < hi:
                    mid = lo + (hi - lo) // 2 
                    
                    if (nums[mid] == target):
	                    # Check if its last element and recurse
                        if mid == hi or nums[mid + 1] != target:
                            return mid
                        else:
                            lo = mid + 1
                    
                    elif (nums[mid] > target):
                        hi = mid - 1
                    
                    else:
                        lo = mid + 1
                    
                if nums[hi] == target:
                    return hi
                else:
                    return -1
        
        
        return [search(nums, target, True), search(nums, target, False)]

```


### Shorter Solution Using Bisect

```python
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        lo = bisect_left(nums, target) # Find the 
        hi = bisect_right(nums, target) 
        
        if lo == len(nums) or nums[lo] != target:
            return [-1, -1]
        else:
            return [lo, hi - 1]
```

---
Link: [[Binary Search]]