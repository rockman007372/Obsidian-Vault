---
tags: LeetCode
topics: Binary Search
difficulty: medium
performance: complete, optimal
date: 2023-01-07 Saturday
---

### Questions

A peak element is an element that is strictly greater than its neighbors.

Given a **0-indexed** integer array `nums`, find a peak element, and return its index. If the array contains multiple peaks, return the index to **any of the peaks**.

You may imagine that `nums[-1] = nums[n] = -∞`. In other words, an element is always considered to be strictly greater than a neighbor that is outside the array.

You must write an algorithm that runs in `O(log n)` time.

### Solution

Simple [[Binary Search]]

```python
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        lo, hi = 0, len(nums) - 1

        while lo < hi:
            mid = lo + (hi - lo) // 2
            
            # if peak, return index
            if mid != 0 and nums[mid] > nums[mid + 1] and nums[mid] > nums[mid - 1]:
                return mid

            if nums[mid] < nums[mid + 1]:
                lo = mid + 1
            else: # nums[mid] >= nums[mid + 1]
                hi = mid # or hi = mid - 1, because we alr check for peak condition above
        
        return lo
```

```Java
public class Solution {
    public int findPeakElement(int[] nums) {
        int l = 0, r = nums.length - 1;
        while (l < r) {
            int mid = (l + r) / 2;
            if (nums[mid] > nums[mid + 1])
                r = mid; // so that we dont miss the peak
            else
                l = mid + 1;
        }
        return l;
    }
}
```