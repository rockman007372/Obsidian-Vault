---
tags: LeetCode
topics: sliding window
difficulty: medium
performance: complete
date: 2023-01-13 Friday
---

## Questions

Given an array of positive integers `nums` and a positive integer `target`, return the **minimal length** of a subarray whose sum is greater than or equal to `target`. If there is no such subarray, return `0` instead.

**Example 1:**
```
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.

```

## Solution

### Sliding Window

Standard [[Fast-Slow Sliding Window]]

Time: O(N)
Space: O(1)

```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        n = len(nums)
        lo = 0
        sum = 0
        res = float('inf')
        for hi in range(n):
            sum += nums[hi]
            
            while sum >= target and lo <= hi:
               res =  min(res, hi - lo + 1)
               sum -= nums[lo]
               lo += 1
        
        return res if res != float('inf') else 0
```
