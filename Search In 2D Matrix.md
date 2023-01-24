---
tags: LeetCode
topics: Binary Search
difficulty: medium
performance: uncomplete
date: 2023-01-07 Saturday
---
[[Binary Search]]
### Questions

You are given an `m x n` integer matrix `matrix` with the following two properties:

-   Each row is sorted in non-decreasing order.
-   The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return `true` _if_ `target` _is in_ `matrix` _or_ `false` _otherwise_.

You must write a solution in `O(log(m * n))` time complexity.

![[Pasted image 20230107230433.png]]

### Solution
##### Treat 2D matrix as a 1D array

Trick is to manipulate the matrix indices to find the middle element:

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        m, n = len(matrix[0]), len(matrix)
        lo, hi = 0, (m * n - 1)

        while lo < hi:
            mid = lo + (hi - lo) // 2
            midVal = matrix[mid // m][mid % m]
            
            if midVal >= target:
                hi = mid
            else:
                lo = mid + 1
        
        return matrix[lo // m][lo % m] == target
```

Time: `O(lg(MN))`
Space: `O(1)`


