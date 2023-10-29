---
tags:
  - LeetCode
  - leetcode
topics: greedy, monotonic stack
difficulty: hard
performance: uncomplete
date: 2023-10-23 Monday
---

## Questions

Input:  `nums[]` and an integer `k`.

The **score** of a subarray `(i, j)` is defined as 

```
score = min(nums[i], nums[i+1], ..., nums[j]) * (j - i + 1)
```

A **good** subarray is a subarray where `i <= k <= j`.

Return _the maximum possible **score** of a **good** subarray._

## Solution

### Greedy solution

- Idea is similar to [[Container with Most Water]]. 
- Observations:
	- want to maximise the minimum number in the subarray
	- want to maximise subarray length
	- given a subarray, if you expand the subarray, minimum number can only decrease, but length of subarray will increase.
	- i <= k <= j => k is like a pivot.
- We use some sort of [[Front-Back Sliding Window]]: expand `left` if `left` > `right`, else expand `right`
	- Why? Assume `left > right`. Any solution that contains `right` must contain `left` too.

```python
class Solution:
    def maximumScore(self, nums: List[int], k: int) -> int:
        # set up sliding window
        i = j = k
        ans = nums[k]
        currMin = nums[k]
        n = len(nums) 
        while i > 0 or j < n - 1:
            if (nums[i - 1] if i > 0 else 0) > \\
	        (nums[j + 1] if j < n - 1 else 0):
                i -= 1
                currMin = min(currMin, nums[i])
            else:
                j += 1
                currMin = min(currMin, nums[j])
            
            ans = max(ans, currMin * (j - i + 1))
        return ans
```

### Monotonic stack

- We make use of [[Monotonic Stack]] to find the first element smaller than `nums[i]` on the left and on the right. 

**Algorithm**

1. Initialize `n = nums.length`, `left` as an array of length `n` with values of `-1`, and an empty `stack`.
2. Iterate `i` from `n - 1` until `0`:
    - While the element at the index at the top of `stack` is greater than `nums[i]`, pop this index from `stack`. Given `j` as the index popped from the `stack`, set `left[j] = i`.
    - Push `i` to `stack`.
3. Initialize `right` as an array of length `n` with values of `n` and reset `stack`.
4. Iterate `i` over the indices of `nums`:
    - While the element at the index at the top of `stack` is greater than `nums[i]`, pop this index from `stack`. Given `j` as the index popped from the `stack`, set `right[j] = i`.
    - Push `i` to `stack`.
5. Initialize `ans = 0`.
6. Iterate `i` over the indices of `nums`:
    - If `left[i] < k` and `right[i] > k`, update `ans` with `nums[i] * (right[i] - left[i] - 1)` if it is larger.

---
Link: [[LeetCode]]
