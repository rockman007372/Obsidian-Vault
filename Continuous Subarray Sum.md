---
tags: LeetCode
topics: modulus, hash, prefix_sum
difficulty: medium
performance: uncomplete
date: 2022-10-26 Wednesday
---

### Questions

Given an integer array nums and an integer k, return true if nums has a continuous subarray of size at least two whose elements sum up to a multiple of k, or false otherwise.

An integer x is a multiple of k if there exists an integer n such that x = n * k. 0 is always a multiple of k.

**Example 1:**

**Input:** nums = [23,2,4,6,7], k = 6
**Output:** true
**Explanation:** [2, 4] is a continuous subarray of size 2 whose elements sum up to 6.

**Example 2:**

**Input:** nums = [23,2,6,4,7], k = 6
**Output:** true
**Explanation:** [23, 2, 6, 4, 7] is an continuous subarray of size 5 whose elements sum up to 42.
42 is a multiple of 6 because 42 = 7 * 6 and 7 is an integer.

### Solution

- Key idea: `x % k = (x + n*k) % k` 
- If the above condition happens, that means we just add to the prefix sum a value that is a multiple of k.
- We make use of a hash table to cache the index of the first time we see a remainder
- Condition to return true: if reminder is seen again & the subarray has length >= 2

```Python
class Solution:
    def checkSubarraySum(self, nums: List[int], k: int) -> bool:
        cache = {0 : 0}
        prefixSum = 0
        for i in range(len(nums)):
            prefixSum += nums[i]
            remainder = prefixSum % k
            
            if remainder in cache:
                if i - cache[remainder] > 0:
                    return True
            else:
                cache[remainder] = i + 1
        
        return False
```

---
Link: [[LeetCode]]