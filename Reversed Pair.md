---
tags:
  - LeetCode
  - leetcode
topics: divide-and-conquer
difficulty: hard
performance: complete, notOnTime
date: 2023-09-19 Tuesday
---

## Questions

Given an integer array `nums`, return _the number of **reversed pairs** in the array_.

A **reverse pair** is a pair `(i, j)` where:

- `0 <= i < j < nums.length` and
- ! `nums[i] > 2 * nums[j]`.

## Solution

This is basically [[Counting Inversions]] with a twist.

```python
class Solution:
    def reversePairs(self, nums: List[int]) -> int:
        count, sortedArr = self.countAndSort(nums)
        print(sortedArr)
        return count
    
    def countAndSort(self, nums) -> (int, List[int]):
        n = len(nums)
        if n == 1:
            return (0, nums)
            
        leftCount, leftArr = self.countAndSort(nums[:n//2])
        rightCount, rightArr = self.countAndSort(nums[n//2:])
        totalCount, totalArr = self.merge(leftArr, rightArr)
        return (leftCount + rightCount + totalCount, totalArr)

    def merge(self, xs, ys):
        m = len(xs)
        n = len(ys)
        
        i, j = 0, 0
        result = []
        count = 0
        
        # count step
        while i < m and j < n:
            if xs[i] <= 2 * ys[j]:
                i += 1
            else: # inversion
                j += 1
                count += m - i
        
        # merge step
        i = j = 0
        while i < m and j < n:
            if xs[i] <= ys[j]:
                result.append(xs[i])
                i += 1
            else: # inversion
                result.append(ys[j])
                j += 1
        
        if i == m and j < n:
            result += ys[j:]
        
        if i < m and j == n:
            result += xs[i:]
        
        return (count, result)
```

---
Link: [[LeetCode]]
