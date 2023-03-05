---
tags: LeetCode
topics: Hash Table, Math
difficulty:
performance: complete, notOnTime
date: 2023-01-09 Monday
---

### Questions

Given an array of `points` where `points[i] = [xi, yi]` represents a point on the **X-Y** plane, return _the maximum number of points that lie on the same straight line_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/25/plane1.jpg)

**Input:** points = `[[1,1],[2,2],[3,3]]`
**Output:** `3`

### Solution

##### My solution - O(N^2)

Algorithm:
1. Fix a point, and calculate the gradient between that point to the rest
2. Save the max number of points sharing the same gradient
3. Mark that point as visited and fix the next point, ignoring the visited points.

```python
class Solution:
    def maxPoints(self, points: List[List[int]]) -> int:
        if len(points) == 1:
            return 1
            
        res = 0
        grads = {}
        
        for i in range(len(points) - 1):
            pivot = points[i]
            for j in range(i + 1, len(points)):
                point = points[j]
                gradient = float('inf')
                if point[0] - pivot[0] != 0:
                    gradient = (point[1] - pivot[1]) / (point[0] - pivot[0]) 
                    
                if gradient not in grads:
                    grads[gradient] = 1
                    
                grads[gradient] += 1
                
            res = max(res, max(grads.values()))
            grads = {}
            
        return res
```

Time: O(N^2)
Space: O(N) - store the hash map

---
Link: [[Hash Table]]
