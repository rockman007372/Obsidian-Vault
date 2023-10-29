---
tags:
  - LeetCode
  - leetcode
topics: backtracking, DP, sliding window
difficulty: medium
performance: complete, notOptimal
date: 2023-09-21 Thursday
---

## Questions

Given an array of int and a value x. In each operation, you can remove either the leftmost or rightmost value in the array, then subtract it from the value x.

Find the minimum # operations to reduce x to 0.

## Solution

### Backtracking (Time Limit Exceeds)

Idea:
- Either remove the first or the last element in each operation => take one action and recurse until reach solution / exceed, then backtrack to take a different solution.
- Notice there are repeated states: whenever you have reduced the array to a certain size before, you do not have to check it again in later recursive steps.

```python
class Solution:
    def minOperations(self, nums: List[int], x: int) -> int:
        res = float('inf')
        cache = set()

        # returns the min number of operations to reduce x to 0
        def backtrack(lo, hi, remaining, count) -> int:
            nonlocal res

            if (lo, hi) in cache:
                return

            cache.add((lo, hi))
            
            if remaining == 0:
                res = min(count, res)
                return

            if lo > hi or remaining < 0:
                
                return 
            
            backtrack(lo + 1, hi, remaining - nums[lo], count + 1)
            backtrack(lo, hi - 1, remaining - nums[hi], count + 1)

        backtrack(0, len(nums) - 1, x, 0)
        return -1 if res == float('inf') else res
```

Time: O(2^n), at each step you have 2 options to take, and there are at most n steps.

However, with memoization, we can potentially cut down the recursion tree by half? not sure, but got TLE :(

Space: O(n^2) - storing all combinations of (lo, hi)
### Sliding Window

Transform the problem into a modified [[Minimum Size Subarray Sum]] problem!

Big idea: find the maximum size of the subarray whose sum = total sum - x.

```python
class Solution:
    def minOperations(self, nums: List[int], x: int) -> int:
        expectedSum = sum(nums) - x

        if expectedSum == 0:
            return len(nums)
            
        if expectedSum < 0:
            return -1
    
        # find the maximum size of subarray whose sum = total sum - x
        maxSize = -1
        lo = 0
        currSum = 0
        for hi in range(len(nums)):

            currSum += nums[hi]
                                     
            while lo <= hi and currSum > expectedSum:
                currSum -= nums[lo]
                lo += 1

            if currSum == expectedSum:
                maxSize = max(maxSize, hi - lo + 1)

        if maxSize == -1:
            return -1
        
        return len(nums) - maxSize
```

Time: O(n)
Space: O(1)


---
Link: [[LeetCode]]
