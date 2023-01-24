---
tags: LeetCode
topics: array, hash
difficulty: medium
performance: uncompleted
date: 2022-12-08 Thursday
---

### Questions

You are given an array of points in the **X-Y** plane `points` where `points[i] = [xi, yi]`.

Return _the minimum area of a rectangle formed from these points, with sides parallel to the X and Y axes_. If there is not any such rectangle, return `0`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/08/03/rec1.JPG)

**Input:** points = `[[1,1],[1,3],[3,1],[3,3],[2,2]]`
**Output:** 4

### Solution

Big idea is to fix any 2 points, and check whether the remaining 2 points exist. This is possible because the conditions dictated that the width and height are parallel to the axes. Finding a pair of 2 points take O(N^2). To find the other 2 points, we can make use of [[HashSet]] which takes O(1) time.

Time: O(N^2)
Space: O(N) - to keep all the points in set

```python
class Solution:
    def minAreaRect(self, points: List[List[int]]) -> int:
        res = float('inf')
        visited = set()

        for (x1, y1) in points:
            for (x2, y2) in visited:
                if (x1, y2) in visited and (x2, y1) in visited: # O(1)
                    area = abs(x1 - x2) * abs(y1 - y2)
                    res = min(res, area) # ensure area is minimum
                    
            visited.add((x1, y1))

        return res if res != float('inf') else 0
```