---
tags: LeetCode, leetcode
topics: heap
difficulty: medium
performance: complete, notOnTime
date: 2023-05-24 Wednesday
---

## Questions

You are given two **0-indexed** integer arrays `nums1` and `nums2` of equal length `n` and a positive integer `k`. You must choose a **subsequence** of indices from `nums1` of length `k`.

For chosen indices `i0`, `i1`, ..., `ik - 1`, your **score** is defined as:

-   The sum of the selected elements from `nums1` multiplied with the **minimum** of the selected elements from `nums2`.
-   It can defined simply as: `(nums1[i0] + nums1[i1] +...+ nums1[ik - 1]) * min(nums2[i0] , nums2[i1], ... ,nums2[ik - 1])`.

Return _the **maximum** possible score._

A **subsequence** of indices of an array is a set that can be derived from the set `{0, 1, ..., n-1}` by deleting some or no elements.

**Example 1:**

**Input:** `nums1 = [1,3,3,2], nums2 = [2,1,3,4], k = 3`
**Output:** 12
**Explanation:** 
The four possible subsequence scores are:
- We choose the indices 0, 1, and 2 with score = (1+3+3) * min(2,1,3) = 7.
- We choose the indices 0, 1, and 3 with score = (1+3+2) * min(2,1,4) = 6. 
- We choose the indices 0, 2, and 3 with score = (1+3+2) * min(2,3,4) = 12. 
- We choose the indices 1, 2, and 3 with score = (3+3+2) * min(1,3,4) = 8.
Therefore, we return the max score, which is 12.

## Solution

### Heap

Idea: 
- Sort the 2 arrays in terms of the second array, in descending order
- Traverse the 2 arrays from left to right while maintaining a min [[Heap]] of constant size k (or k - 1). 
- ! Before we add a new element to the heap, we remove the smallest value in the heap

Time: O(nlogn)
- O(nlogn) to sort the 2 arrays
- O(k) to heapify k elements
- O(nlogk) to push and pop into the heap

Space: O(n + k)
- O(n) to store paired array
- O(k) to store heap

```python
class Solution:
    def maxScore(self, nums1: List[int], nums2: List[int], k: int) -> int:
        sorted_nums = sorted(zip(nums1, nums2), key=lambda x : -x[1]) 

        # maintain a min heap of the first k elements
        minHeap = [pair[0] for pair in sorted_nums[:k]]
        heapq.heapify(minHeap)
        max_sum = sum(minHeap)

        # initial max score of the first k elems
        res = max_sum * sorted_nums[k - 1][1]  

        # process the rest of the array
        for val1, val2 in sorted_nums[k : len(nums2)]:

            # maintain the max k elements
            minVal = heapq.heappop(minHeap)
            heapq.heappush(minHeap, val1)
            max_sum = max_sum - minVal + val1

            res = max(res, max_sum * val2)
        
        return res
```

>[!learning points]
> - `sorted` function takes in a key, which is very similar to a comparable (basically dictating what value the sort function uses to sort). There is no comparator.

---
Link: [[LeetCode]]
