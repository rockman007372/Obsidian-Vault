---
tags: LeetCode
topics: backtracking
difficulty: medium
performance: complete
date: 2022-07-27 Wednesday
---

## Questions

Given an integer array `nums` that may **contain duplicates**, return _all possible subsets (the power set)_.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

```
**Input:** nums = [1,2,2]
**Output:** [[],[1],[1,2],[1,2,2],[2],[2,2]]
```

**Example 2:**

```
**Input:** nums = [0]
**Output:** [[],[0]]
```


Key notes: 
- All nums are NOT unique, hence there can be duplicates (eg. `[1, 2, 2] -> [1, 2] and [1, 2] can be considered as 2 different sets`)
- Compare this with [[Combination Sum I]] and [[Subsets]], which has no duplicates in nums `int[]`

## Solution
### Backtracking
Idea: 
- To prevent duplicate, we must first *sort the nums array*.
- Solution similar to [[Subsets]]

Time: `O(N * 2 ^ N + NlgN)`
Space: `O(N)`

```Java
class Solution {
    private List<List<Integer>> res;
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        res = new ArrayList<>();
        Arrays.sort(nums); // ensure duplicates are packed
        helper(new LinkedList<Integer>(), nums, 0);
        return res;
    }
    
    private void helper(LinkedList<Integer> subset, int[] nums, int idx) {
        res.add(new LinkedList<>(subset));                
        
        for (int i = idx; i < nums.length; i++) {
            // prevent duplicated subsets
            if (i != idx && nums[i] == nums[i - 1]) {
                continue;
            }
            subset.add(nums[i]);
            helper(subset, nums, i + 1);
            subset.removeLast();
        }     
    }
}
```

```python
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        
        # sortedNums = sorted(nums)
        nums.sort()
        res = []

        def backtrack(idx: int, subset: List[int]):
            nonlocal res
            
            res.append(list(subset))

            for i in range(idx, len(nums)):
                if i == idx or nums[i] != nums[i - 1]:
                    subset.append(nums[i])
                    backtrack(i + 1, subset)
                    subset.pop()

        backtrack(0, [])
```

### Dynamic Programming / Cascading 
Idea: 
- Built next subsets from previously built subsets
- How to prevent duplicates? -> Whenever a value is encountered for the first time, we add it to all the existing subsets. Then onwards we add its duplicates only to the subsets created in the previous step.

![[Pasted image 20220727210833.png||800]]
![[Pasted image 20220727210849.png||800]]

```Java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> subsets = new ArrayList<>();
        subsets.add(new ArrayList<Integer>());

        int subsetSize = 0;

        for (int i = 0; i < nums.length; i++) {
            int startingIndex = (i >= 1 && nums[i] == nums[i - 1]) ? subsetSize : 0;
            // subsetSize refers to the size of the subset in the previous step. This value also indicates the starting index of the subsets generated in this step.
            subsetSize = subsets.size();
            for (int j = startingIndex; j < subsetSize; j++) {
                List<Integer> currentSubset = new ArrayList<>(subsets.get(j));
                currentSubset.add(nums[i]);
                subsets.add(currentSubset);
            }
        }
        return subsets;
    }
}
```

---
Tags: [[LeetCode]] - [[Backtracking]]
