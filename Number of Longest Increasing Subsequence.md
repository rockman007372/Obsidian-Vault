---
tags: LeetCode, leetcode
topics: dp, lis
difficulty: medium
performance: uncomplete
date: 2023-07-22 Saturday
---
See also: [[LIS invariants]]

## Questions

Given an integer array `nums`, return _the number of longest increasing subsequences._

**Notice** that the sequence has to be **strictly** increasing.

## Solution

Idea:
- Store 2 dp, `lis` and `count`. 
- `lis[i]` stores the length of lis that ends at index i
- `count[i]` stores the number of lis that ends at index i
- While we update `lis` (find a longer lis), we also update `count` accordingly.

Time: O(N^2)
Space: O(N)

```python
class Solution:
    def findNumberOfLIS(self, nums: List[int]) -> int:
        n = len(nums)
        lis = [1] * n
        count = [1] * n # the number of LISs ending at index i

        for i in range(n):
            for j in range(i):
                
                # found a new (longer) LIS
                if nums[i] > nums[j] and lis[j] + 1 > lis[i]:
                    lis[i] = lis[j] + 1
                    count[i] = count[j] # reset 

                # found an LIS of same length
                elif nums[i] > nums[j] and lis[j] + 1 == lis[i]: 
                    count[i] += count[j]
        
        longestLen = max(lis)
        res = 0
        for i in range(n):
            if lis[i] == longestLen:
               res += count[i]

        return res 
```


---
Link: [[LeetCode]]
