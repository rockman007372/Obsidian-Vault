---
tags: LeetCode, leetcode
topics: binarysearch, twopointers
difficulty: hard
performance: uncomplete
date: 2023-05-18 Thursday
---

## Questions
Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return **the median** of the two **sorted** arrays.

The overall run time complexity should be `O(log(min(m,n))`.

**Example 1:**

```
Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.
```

**Example 2:**

```
Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
```


## Solution

### Binary Search 


Key points:

1.  We want to make two cuts, separating nums1 into `[...L1 | R1...]` and nums2 into `[...L2 | R2...]` respectively, so that `[...L1] + [...L2]` has equal number of elements as `[R1...] + [R2...]`. Our goal is to find such cutting positions that give us the median values.
2.  For an array of length `N`, there are `2*N + 1` different cutting positions.
3.  Cutting on a gap is simple. Cutting on a number means both left half and right half get the number.
4.  With two arrays, a valid cutting position that gives the median can be **ANY** cutting position of the shorter array. This is not true for the longer array. Therefore, **we always cut the shorter array**, and then calculate the cutting position of longer array directly (by using the fact that each half has the same number of cutting positions). We want to make nums1 always point to the shorter array for convenience.
5.  Using [[Binary Search]], If L1 > R2, we know current cutting position is incorrect. A valid cutting position for median should be on the **left** half of nums1.
6.  If L2 > R1, we know current cutting position is incorrect. A valid cutting position for median should be on the **right** half of nums1.
7.  if L1 < R2 and L2 < R1, we are good. `median = (max(L1, L2) + min(R1, R2)) / 2`

More detailed [explanation](https://leetcode.com/problems/median-of-two-sorted-arrays/solutions/2471/very-concise-o-log-min-m-n-iterative-solution-with-detailed-explanation/)

Time: O(log(min(m, n)))
Space: O(1)

```python
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        n = len(nums1)
        m = len(nums2)
        if m < n: 
            return self.findMedianSortedArrays(nums2, nums1)
        
        lo = 0
        hi = 2 * n 

        while lo <= hi:
            cut1 = lo + (hi - lo) // 2
            cut2 = m + n - cut1 # make use of equal halves

            L1Index = (cut1 - 1) // 2 # edge case: index < 0
            R1Index = cut1 // 2       # edge case: index = n
            L2Index = (cut2 - 1) // 2 # edge case: index < 0
            R2Index = cut2 // 2       # edge case: index = m

            L1 = float('-inf') if L1Index < 0 else nums1[L1Index]
            R1 = float('inf') if R1Index == n else nums1[R1Index]
            L2 = float('-inf') if L2Index < 0 else nums2[L2Index]
            R2 = float('inf') if R2Index == m else nums2[R2Index]

            if L1 <= R2 and L2 <= R1:
                return (max(L1, L2) + min(R1, R2)) / 2
            elif L1 > R2:
                hi = cut1 - 1
            elif L2 > R1:
                lo = cut1 + 1

        return -1 # no solution
```

---
Link: [[LeetCode]]
