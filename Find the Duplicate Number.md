---
tags:
  - LeetCode
  - leetcode
topics: cycle
difficulty: hard
performance: uncomplete
date: 2023-09-19 Tuesday
---

## Questions

Given an array of (n + 1) integers such that:
- Every element is within the range `[1, n + 1]`
- There is exactly 1 repeated integer (can be repeated **2 or more**.

Find the repeated number such that 
- No modification of the array
- Constant extra space O(1)

## Solution

Big idea:
- Transform the problem into a linked list: node `x` -> node `nums[x]`.
- If `x` is a duplicated number, `x` will be reached many times (cycle starts at x).
- Modified [[Floyed's Cycle Finding Algorithm]] to find the entrance of the cycle.
	- Phase 1: find the intersection of the fast and slow pointers using Floyed.
	- Phase 2: slow down the fast pointer, and reset the position of the slow pointer. Race the 2 pointers once again to find the entrance of the cycle.


```python
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        
        # phase 1: find the intersection in cycle
        slow = fast = nums[0]
        while True:
            slow = nums[slow]
            fast = nums[nums[fast]]
            
            if slow == fast:
                break

        # phase 2: find the entrance of cycle = duplicate item
        slow = nums[0]
        while slow != fast:
            slow = nums[slow]
            fast = nums[fast]
        return slow
```

Proof:

After phase 1:
- distance `slow` travels = F + a, where F is the distance to reach cycle entrance, a is the distance from entrance to insersection.
- distance `fast` travels = F + nC + a, where C is the cycle length
- Since `fast` travels twice as many nodes as `slow`: 2(F + a) = F + nC + a 
- Hence F + a = nC

After phase 2:
- To reach entrace, `slow` must travel F steps. 
- In F steps, `fast` will have reached F + a + F = nC + F = F?? idk man


---
Link: [[LeetCode]]
