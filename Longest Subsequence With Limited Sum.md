---
tags: LeetCode
topics: PrefixSum, BinarySearch
difficulty: easy
performance: notOptimal, completed
date: 2022-12-25 Sunday
---
Related Topics: [[Prefix Sum]], [[Binary Search]]

### Questions

You are given an integer array `nums` of length `n`, and an integer array `queries` of length `m`.

Return _an array_ `answer` _of length_ `m` _where_ `answer[i]` _is the **maximum** size of a **subsequence** that you can take from_ `nums` _such that the **sum** of its elements is less than or equal to_ `queries[i]`.

A **subsequence** is an array that can be derived from another array by deleting some or no elements without changing the order of the remaining elements.

### Solution

#### Brute Force: Sort then Find Sum

```python
class Solution:
    def answerQueries(self, nums: List[int], queries: List[int]) -> List[int]:
        nums.sort()
        res = []

        for maxSum in queries:
            count = 0
            subSum = 0
            for num in nums:
                subSum += num
                if subSum > maxSum:
                    break
                count += 1
            res.append(count)

        return res
```

Time: 
- Sorting takes O(NlogN)
- Finding the right sum takes at most O(N), hence O(M.N) in total
- Total: O(NlgN + MN)

Space: O(N) or O(lgN) depending on sorting implementation

#### Prefix Sum then Binary Search

By using Binary Search on the Prefix Sum of the nums array, we can cut down the search for the minimum sum to lg(N). Hence runtime is reduced to O(N.lgN + M.lgN) = O((M + N).lgN)

```python
class Solution:
    def answerQueries(self, nums: List[int], queries: List[int]) -> List[int]:
        nums.sort()
        res = []

        # Get the prefix sum
        prefix = []
        preSum = 0
        for num in nums:
            preSum += num
            prefix.append(preSum)

        # Binary Search through the prefix sum array
        for maxSum in queries:
            count = bisect_right(prefix, maxSum) # find the maximum element smaller or equal to maxSum
            res.append(count)

        return res
```





