---
tags: LeetCode
topics: two pointers
difficulty: medium
performance: complete
date: 2023-01-09 Monday
---
[[3Sum]]

### Questions

Given an integer array `nums` of length `n` and an integer `target`, find three integers in `nums` such that the sum is closest to `target`.

Return _the sum of the three integers_.

You may assume that each input would have exactly one solution.

**Example 1:**

**Input:** nums = [-1,2,1,-4], target = 1
**Output:** 2
**Explanation:** The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

### Solution

##### Two Pointers

```python
class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        nums.sort()
        min_diff = float('inf')
        res = 0
        for x in range(len(nums) - 2):
            y = x + 1
            z = len(nums) - 1
            while y < z:
                total = nums[x] + nums[y] + nums[z]
                diff = abs(total - target)
                
                if diff == 0:
                    return target
                elif total < target:
                    y += 1
                elif total > target:
                    z -= 1
                    
                if diff < min_diff:
                    res = total
                    min_diff = diff
                
        return res
```

```python
class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        diff = float('inf')
        nums.sort()
        for i in range(len(nums)):
            lo, hi = i + 1, len(nums) - 1
            while (lo < hi):
                sum = nums[i] + nums[lo] + nums[hi]
                if abs(target - sum) < abs(diff): # do abs comparison here
                    diff = target - sum # no need to keep another res variable
                if sum < target:
                    lo += 1
                else:
                    hi -= 1
            if diff == 0:
                break
        return target - diff
```

Time: O(N^2)
Space: O(N) or O(NlgN) due to sorting

