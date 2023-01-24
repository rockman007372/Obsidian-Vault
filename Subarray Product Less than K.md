---
tags: LeetCode
topics: Sliding Window
difficulty: medium
performance: uncomplete
date: 2023-01-12 Thursday
---

## Questions

Given an array of integers `nums` and an integer `k`, return _the number of contiguous subarrays where the product of all the elements in the subarray is strictly less than_ `k`.

**Example 1:**

```
**Input:** nums = [10,5,2,6], k = 100
**Output:** 8
**Explanation:** The 8 subarrays that have product less than 100 are:
[10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6]
Note that [10, 5, 2] is not included as the product of 100 is not strictly less than k.
```

**Example 2:**

```
**Input:** nums = [1,2,3], k = 0
**Output:** 0
```

## Solution

### Sliding Window

SO ELEGANT

Key idea: 
- Sliding window is the maximum subarray product that is strictly less than K
- The number of additional valid subarrays = `hi - lo + 1`

Time: O(N)
Space: O(1)

```python
class Solution:
    def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
        
        lo, hi = 0, 0
        count = 0
        prod = 1

        while hi < len(nums):
            prod *= nums[hi]

            while prod >= k and lo <= hi:
                prod /= nums[lo]
                lo += 1
            
            count += (hi - lo + 1) # the additional number of subarrays
            hi += 1

        return count
        
    
        
        # # O(N^2) solution: expand window until product exceed,
        # # then move to the next index and reset window

        # res = 0
        # for i in range(len(nums)):
        #     product = nums[i]
        #     if product < k:
        #         res += 1
        #     for j in range(i + 1, len(nums)):
        #         product *= nums[j] 
        #         if product < k:
        #             res += 1
        #         else:
        #             break

        # return res
        
        
        # # Naive solution: O(N * Summation(1/N))
        # res = 0
        # for size in range(1, len(nums) + 1):
        #     for i in range(len(nums) - size + 1):
        #        product = reduce(lambda x, y : x * y, nums[i: i + size])
        #        if product < k:
        #            res += 1

        # return res 
```
