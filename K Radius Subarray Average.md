---
tags: LeetCode, leetcode
topics: slidingWindow, prefixSum
difficulty: medium
performance: complete, notOptimal
date: 2023-06-20 Tuesday
---

## Questions

You are given a **0-indexed** array `nums` of `n` integers, and an integer `k`.

The **k-radius average** for a subarray of `nums` **centered** at some index `i` with the **radius** `k` is the average of **all** elements in `nums` between the indices `i - k` and `i + k` (**inclusive**). If there are less than `k` elements before **or** after the index `i`, then the **k-radius average** is `-1`.

Build and return _an array_ `avgs` _of length_ `n` _where_ `avgs[i]` _is the **k-radius average** for the subarray centered at index_ `i`.

Example:

**Input:** nums = `[7,4,3,9,1,8,5,2,6]`, k = 3
**Output:** `[-1,-1,-1,5,4,4,-1,-1,-1]
`
## Solution

### Prefix Sum

```python
class Solution:
    def getAverages(self, nums: List[int], k: int) -> List[int]:
        # build subarray prefix sum
        n = len(nums)
        prefixSum = [0] * (n + 1)
        prefixSum[0] = 0
        for i in range(0, n):
            prefixSum[i + 1] = nums[i] + prefixSum[i]
        
        # build average array
        aveArray = [-1] * n
        length = 2 * k + 1
        for i in range(k, n - k):
            aveArray[i] = (prefixSum[i + k + 1] - prefixSum[i - k]) // length

        return aveArray
```

Space: O(N)

### Sliding Window

We can further reduce space to O(1) by sliding the window of size `2k + 1` by one in each iteration.

```python
class Solution:
    def getAverages(self, nums: List[int], k: int) -> List[int]:        
        n = len(nums)
        aveArray = [-1] * n
        length = 2 * k + 1
        currSum = sum(nums[0:length])
        for i in range(k, n - k):
            aveArray[i] = currSum // length

            if i == (n - k - 1):
                break

            currSum = currSum + nums[i + k + 1] - nums[i - k] 

        return aveArray
```

---
Link: [[LeetCode]]

