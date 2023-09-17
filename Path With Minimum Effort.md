---
tags:
  - LeetCode
  - leetcode
topics: SSSP
difficulty: medium
performance: uncomplete
date: 2023-09-17 Sunday
---

## Question

Input: 2d array, each entry stores the height of the hill. 
Output: the minimum effort to traverse from top left to bottom right.

Effort = max absolute difference between 2 adjacent hills = max(abs(i, j)) for all i and j = i + 1.

![[Pasted image 20230917103027.png]]

Min effort = 1
## Solution

We make use of a modified [[Dijkstra's Algorithm]]:
- We keep a priority queue of nodes ordered by the estimated min effort to reach that node (instead of estimated min distance)
- Once a node is popped, the minimum effort to reach the node has been found. This works because once a node is popped, you will not update that node ever again. Exploring more nodes will not lower the min effort of previously popped nodes.
- Relax function: update priority in PQ.

```python
class Solution:
    def minimumEffortPath(self, heights: List[List[int]]) -> int:
        ROWS, COLS = len(heights), len(heights[0])
        DIRS = [[1, 0], [-1, 0], [0, 1], [0, -1]]
        
        estimates = [[float('inf')] * COLS for _ in range(ROWS)]
        estimates[0][0] = 0
        pq = [(0, 0, 0)]
        heapq.heapify(pq)
        
        while pq:
            effort, x, y = heapq.heappop(pq)
	        
	        # goal check
            if (x, y) == (ROWS - 1, COLS - 1):
                return effort
                
            for (dx, dy) in DIRS:
                neighbor_x = x + dx
                neighbor_y = y + dy
                
                if neighbor_x < 0 or neighbor_x == ROWS 
	                or neighbor_y < 0 or neighbor_y == COLS:
                    continue
                
                # relax edges if valid
                difference = 
	                abs(heights[neighbor_x][neighbor_y] - heights[x][y])
	                
                estimated_effort = max(difference, estimates[x][y])
                
                if estimates[neighbor_x][neighbor_y] > estimated_effort:
                    estimates[neighbor_x][neighbor_y] = estimated_effort
                    heapq.heappush(pq, 
	                    (estimated_effort, neighbor_x, neighbor_y))
	            
        return 0 # never reach
```


Time: 
- number of nodes = V = mn
- max number of edges = E = 4mn 
- Djikstra: O(ElogV) = O(mnLogmn)

Space: O(mn) to store estimates + queue

>[!implementation notes]
> - Ideally, for updating the priority queue, we must delete the old value and reinsert with the new `maxDifference` value. 
> - But, as we know that the updated maximum value is always lesser than the old value and would be popped from the queue and visited before the old value, we could save time and avoid removing the old value from the queue.

---
Link: [[LeetCode]]
