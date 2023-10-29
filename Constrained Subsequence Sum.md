---
tags:
  - LeetCode
  - leetcode
topics: DP, heap, deque
difficulty: hard
performance: complete, notOnTime
date: 2023-10-22 Sunday
---
[Link](https://leetcode.com/problems/constrained-subsequence-sum/description/?envType=daily-question&envId=2023-10-21) 

## Questions

Input: an integer array `nums` and an integer `k`

Output: maximum sum of a **non-empty** subsequence of that array such that: 

```
Consider 2 consecutive element in the subsequence with actual index i and j in the original array, the condition i - j <= k must be satisfied.
```


```
Input: nums = [10,-2,-10,-5,20], k = 2
Output: 23
Explanation: The subsequence is [10, -2, -5, 20].
```
## Solution

### Max Heap

```
observations: you cannot remove k consecutive numbers
----

DP[i] = max subsequence sum btw 0 and i, assuming i is in the subsequence

DP[i] = max(dp[i - j]) + num[i] for j in [1, k] and i - j >= 0

DP[0] = num[0]

how to find max(dp[j]) for j in range(i - k, i - 1) most efficiently?

=> keep a max heap of the last k indices!
=> what if there more than k elements in the heap?
=> we need to store index of the element, and pop the top until the index is in range
```

```python
class Solution:
    def constrainedSubsetSum(self, nums: List[int], k: int) -> int:
        heap = [(-nums[0], 0)] # (sum, index)
        heapq.heapify(heap)
        
        res = nums[0]
        for i in range(1, len(nums)):
            while heap and heap[0][1] < i - k:
                heapq.heappop(heap)
            
            # ignore previous sum if negative
            currSum = max(0, -heap[0][0]) + nums[i] 
            res = max(res, currSum)
            heapq.heappush(heap, (-currSum, i) )
            
        return res
```

Time: O(NlogN)
Space: O(N)

### Monotonic deque

We can reduce the time complexity to find the max sum of the last k indices to O(1), using a deque sorted in decreasing order (monotonic).

Whenever we push a `dp[i]` into the deque, we also pop all the `dp[j]` values that are smaller than `dp[i]`. This is because they will not be checked again in future iteration. 

Number of times of pushing and popping all the elements in `nums` is at most 2. Hence **each operation costs O(1) amortized.**

```python
class Solution:
    def constrainedSubsetSum(self, nums: List[int], k: int) -> int:
        
        dequeue = deque()
        dequeue.append((nums[0], 0)) # stores (dp[i], [i]) in deque

        res = nums[0]
        for i in range(1, len(nums)):
            while dequeue[0][1] < i - k:
                dequeue.popleft()

             # ignore previous sum if negative
            currSum = max(0, dequeue[0][0]) + nums[i]
            res = max(res, currSum)

            while dequeue and dequeue[-1][0] < currSum:
                dequeue.pop()

            dequeue.append( (currSum, i) )

        return res
```





---
Link: [[LeetCode]]
