---
tags: LeetCode, leetcode
topics: permutation, backtracking, recursion
difficulty: medium
performance: uncomplete
date: 2023-01-22 Sunday
---

## Questions

Given a collection of numbers, `nums`, that might contain duplicates, return _all possible unique permutations **in any order**._

**Example 1:**

```
Input: nums = [1,1,2]
Output: [[1,1,2], [1,2,1], [2,1,1]]
```

**Example 2:**

```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

## Solution

### Recursion - CS1101S Style

Idea: 
- For each element in nums, remove it from the list, call permutation on that sublist, then append the element to the start of each subpermutation
- To prevent duplicate, sort the nums and make sure we dont swap duplicated elements to the start
- This is actually the same as [[Backtracking]]

```python
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:        
        return self.sortedPermute(sorted(nums)) # O(NlgN)
        

    def sortedPermute(self, nums: List[int]): 

        if not nums:
            return [[]]
        
        res = []

        for i in range(len(nums)):
            # prevent duplicate
            if i > 0 and nums[i] == nums[i - 1]:
                continue
            
            subpermutes = self.permuteUnique(nums[:i] + nums[i + 1:])

            for permute in subpermutes:
                permute = [nums[i]] + permute # add the head to each sub-permutation
                res.append(permute)

        return res
```

Time: `O(N! * N)`
Space: O(?)

### Backtracking

- Same ideas as [[Permutation (Leet)]], only now we have to deal with duplicates
- Not sure if we can sort to solve this, but I swap the elements in place and the conditions to not swap is affected somehow
- ! Leetcode solution uses a hashset to prevent swapping duplicated element, by iterating through the `keyset` and not `nums`
- Keep track of a counter and only swap element as the head if `counter[num] > 0`

![[Pasted image 20230122025220.png]]


```python
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        res = []

        if not nums:
            return [[]]

        counter = Counter(nums)

        def backtrack(permute: List[int], counter):

            if len(permute) == len(nums):
                res.append(list(permute))
            else:
                for num in counter.keys(): # only choose unique element as head
                    if counter[num] > 0:
                        permute.append(num)
                        counter[num] -= 1

                        backtrack(permute, counter)

                        permute.pop()
                        counter[num] += 1
               
        backtrack([], counter)
        return res
```


Time: `O(N! * N)`
Space: `O(N)`

---
Link: [[LeetCode]]
