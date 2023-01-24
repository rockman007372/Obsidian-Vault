---
tags: LeetCode
topics: greedy, intervals
difficulty: medium
performance: uncomplete
date: 2023-01-06 Friday
---

### Questions

Input:
Output: 

### Solution

Key idea: sort the balloons by the **upper bound**.

![[Pasted image 20230106014044.png]]

One could always track the end of the current balloon, and ignore all the balloons which end before it. 

Once the current balloon is ended (= the next balloon starts after the current balloon), one has to increase the number of arrows by one and start to track the end of the next balloon.

```python
class Solution:
    def findMinArrowShots(self, points: List[List[int]]) -> int:
        if not points:
            return 0

        sorted_points = sorted(points, key=lambda x : x[1])

        count = 1
        upper = sorted_points[0][1]
        for point in sorted_points:
            if point[0] > upper:
                count += 1
                upper = point[1]
            
        return count 
```

Time: O(NlgN)
Space: O(N) or O(lgN)