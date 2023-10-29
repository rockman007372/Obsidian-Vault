---
tags:
  - LeetCode
  - leetcode
topics: stack, array
difficulty: hard
performance: complete, notOptimal
date: 2023-09-30 Saturday
---

## Questions

Given an array of `n` integers `nums`, a **132 pattern** is a subsequence of three integers `nums[i]`, `nums[j]` and `nums[k]` such that
- `i < j < k` 
- `nums[i] < nums[k] < nums[j]`.

Return `true` if there is a **132 pattern** in `nums`, otherwise, return `false`.

## Solution

O(n^3) brute force solution: find every tuples of 3.

Now, we notice some important observations:
- We want `nums[i]` to be as small as possible.
- We want `nums[j]` to be as big as possible.
- `nums[k]` is in the range `(nums[i], nums[j])`

This inspires us for the O(n^2) solution:
1. Fix j, hence fix aj
2. ai is the smallest element in `nums[:j]`
3. ak is the element in `nums[j+1:]`  such that its in the range (ai, aj)

We can reduce runtime further to O(n) using preprocessing and a stack!
- Preprocess the minimum values of the subarray
- Stack stores the potential values of ak in ascending order from the top. 

When we peek the stack, the top value can either be:
- greater than aj: all the values in stack is not in range since its in ascending order => push aj into stack because aj is now a potential ak in future iterations.
- less than ai: this value is not in range => we keep popping the stack until the top value is more than ai (is this not O(N) ?)
- within our range => return true

Invariants:
- The stack is sorted at all time.
- The minimum value (ai) either stays the same or increases in future operations
- Stack always store potential ak values in the next iteration.

```python
class Solution:
    def find132pattern(self, nums: List[int]) -> bool:

        # preprocess min values so far => potential ai
        minSubarray = [nums[0]] * len(nums)
        for i in range(1, len(nums)):
            minSubarray[i] = min(nums[i], minSubarray[i - 1])
        
        stack = []
        for j in range(len(nums) - 1, 0, -1):
            ai = minSubarray[j]
            aj = nums[j]
            
            if aj <= ai:
                continue

            # check potential ak    
            if (not stack) or (stack[-1] >= aj):
                stack.append(aj)
                continue
        
            # else, stack[-1] <= ai:
            while stack and stack[-1] <= ai:
                stack.pop()
            
            if stack and stack[-1] > ai:
                return True 

        return False
```

Why is runtime O(N)? **At most n elements can be pushed and popped off the stack in total!**

---
Link: [[LeetCode]]
