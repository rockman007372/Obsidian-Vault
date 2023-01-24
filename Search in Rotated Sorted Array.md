2022-06-05 16:44
Tags: [[LeetCode]] - [[Binary Search]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
### 2-pass Binary Search
+ Find the rotation pivot index using [[Binary Search]] 
	+ How? either [[Find Minimum in Rotated Sorted Array]] OR compare to the element to its right (nums[mid  + 1])
+ Binary search on appropriate half using the pivot index
  
```Java
  class Solution {
    public int binarySearch(int[] nums, int target, int lo, int hi) {
        int mid = lo + (hi - lo) / 2;
        if (lo < hi) {
            if (nums[mid] == target) return mid;
            if (nums[mid] > target) {
                return binarySearch(nums, target, lo, mid);
            } else {
                return binarySearch(nums, target, mid + 1, hi);
            }
        }
        return nums[lo] == target ? lo : -1;
    }
    
    public int pivotSearch(int[] nums) {
        int lo = 0;
        int hi = nums.length - 1;
        int mid;
        while (lo < hi) {
            mid = lo + (hi - lo) / 2;
            if (nums[mid] >= nums[0]) {
	            lo = mid + 1;
            } else {
                hi = mid;
            }
        }
        return lo;
    }

	// Another method to find rotate index
	public int find_rotate_index(int left, int right) {
	    if (nums[left] < nums[right])
			return 0;
	    while (left <= right) {
			int pivot = (left + right) / 2;
		    if (nums[pivot] > nums[pivot + 1])
		        return pivot + 1;
		    else {
		        if (nums[pivot] < nums[left])
			        right = pivot - 1;
			    else
			        left = pivot + 1;
			    }
	    }
	    return 0;
	}
        
    public int search(int[] nums, int target) {
        int lo = 0;
        int hi = nums.length - 1;
        if (nums[lo] < nums[hi]) {
            return binarySearch(nums, target, lo, hi);
        } else {
            // search for pivot index
            int pivotIndex = pivotSearch(nums);
            
            // binary search the array before or after pivot index
            if (target < nums[0]) {
                return binarySearch(nums, target, pivotIndex, nums.length - 1);
            } else {
                return binarySearch(nums, target, 0, pivotIndex - 1);
            }
        }  
    }
}
```

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        
        def BS(a, x, lo, hi):
            p = bisect_left(nums, target, lo=lo, hi=hi) 
            if p != hi and a[p] == x:
                return p
            else:
                return -1

        if nums[0] <= nums[-1]:
            return BS(nums, target, lo=0, hi=len(nums))

        # find the pivot k using binary search
        lo = 0
        hi = len(nums) - 1

        k = -1
        while lo < hi:
            mid = lo + (hi - lo) // 2            
            if nums[mid] > nums[mid + 1]:
                k = mid + 1 # index of smallest element
                break
            elif nums[mid] <= nums[0]:
                hi = mid
            else: # nums[mid] > nums[0]
                lo = mid + 1

        # apply BS on the correct segment of nums to find target
        
        if target >= nums[0]:
            return BS(nums, target, lo = 0, hi = k)
        else:
            return BS(nums, target, lo = k, hi = len(nums))
```

### One-pass Binary Search
+ Add some additional _condition checks_ in the normal binary search in order to better _narrow down_ the scope of the search in one pass call
+ Check whether target is in which side of the rotated array 

```Java
class Solution {
    public int search(int[] nums, int target) {
        int lo = 0;
        int hi = nums.length - 1;
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] == target) return mid;
            
            // if cutoff is on the right, we check if 
            // target is between lo and mid
            if (nums[mid] >= nums[lo]) {
                if (nums[mid] > target && nums[lo] <= target) {
                    hi = mid;
                } else {
                    lo = mid + 1;
                }
                
            // if cutoff is on the left, we check if 
            // target is between mid and hi
            } else if (nums[mid] < nums[lo]) {
                if (nums[mid] < target && target <= nums[hi]) {
                    lo = mid + 1;
                } else {
                    hi = mid;
                }
            }   
        }
        return nums[lo] == target ? lo : -1;
    }
}
```

