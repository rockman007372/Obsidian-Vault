---
tags: LeetCode
topics: two pointers
difficulty: medium
performance: uncomplete
date: 2023-01-10 Tuesday
---

### Questions

You are given two lists of closed intervals, `firstList` and `secondList`, where `firstList[i] = [starti, endi]` and `secondList[j] = [startj, endj]`. Each list of intervals is pairwise **disjoint** and in **sorted order**.

Return _the intersection of these two interval lists_.

A **closed interval** `[a, b]` (with `a <= b`) denotes the set of real numbers `x` with `a <= x <= b`.

The **intersection** of two closed intervals is a set of real numbers that are either empty or represented as a closed interval. For example, the intersection of `[1, 3]` and `[2, 4]` is `[2, 3]`.

### Solution

![[Pasted image 20230110151431.png]]

![[Pasted image 20230110151443.png]]

Big ideas:
- Criss-cross condition to detect overlapping 
- Squeeze overlapping area to find the intersection
- Increment pointers based on the upper limit of interval

```python
class Solution:
    def intervalIntersection(self, firstList: List[List[int]], secondList: List[List[int]]) -> List[List[int]]:

        i, j = 0, 0
        overlaps = []

        while i < len(firstList) and j < len(secondList):
            interval1 = firstList[i]
            interval2 = secondList[j]

            # Check for overlap through criss-cross condition
            if interval1[0] <= interval2[1] and interval1[1] >= interval2[0]:
                # get overlapping portion by squeezing overlap area
                lo = max(interval1[0], interval2[0])
                hi = min(interval1[1], interval2[1])
                overlaps.append([lo, hi])
            
            # increment pointer with smallest endpoint
            if interval1[1] < interval2[1]:
                i += 1
            else:
                j += 1
        
        return overlaps
```

Time: O(M + N)
Space: O(M + N) to store overlaps

##### Another way to detect overlapping segment

```python
class Solution:
    def intervalIntersection(self, A: List[List[int]], B: List[List[int]]) -> List[List[int]]:
        ans = []
        i = j = 0

        while i < len(A) and j < len(B):
            # Let's check if A[i] intersects B[j].
            # lo - the startpoint of the intersection
            # hi - the endpoint of the intersection
            lo = max(A[i][0], B[j][0])
            hi = min(A[i][1], B[j][1])
            if lo <= hi:
                ans.append([lo, hi])

            # Remove the interval with the smallest endpoint
            if A[i][1] < B[j][1]:
                i += 1
            else:
                j += 1

        return ans
```