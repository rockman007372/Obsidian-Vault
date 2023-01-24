2022-06-05 16:44
Tags: [[LeetCode]], [[Binary Search]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

### Main Points
- Very similar to [[Search in Rotated Sorted Array]]
- We have to find inflexion point using [[Binary Search]]

```Java
class Solution {
    public int findMin(int[] nums) {
        int lo = 0;
        int hi = nums.length - 1;
        if (nums[lo] <= nums[hi]) {
            return nums[lo];
        }
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            
            // check inflection point
            if (nums[mid] > nums[mid + 1]) {
                return nums[mid + 1];
            }               
            if (nums[mid] < nums[mid - 1]) {
                return nums[mid];
            }
            
            // half the search
            if (nums[mid] < nums[0]) {
                hi = mid;
            } else {
                lo = mid + 1;
            }
        }
        return nums[lo];
    }
}
```

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:

        if nums[0] < nums[-1]:
            return nums[0]

        lo, hi = 0, len(nums) - 1
        while lo < hi:
            mid = (lo + hi) // 2
            if nums[mid] > nums[mid + 1]:
                return nums[mid + 1]
            
            if nums[mid] > nums[lo]:
                lo = mid + 1
            else:
                hi = mid
        
        return nums[lo]
```