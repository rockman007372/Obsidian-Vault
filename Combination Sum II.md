---
tags: LeetCode, leetcode
topics: backtracking
difficulty: medium
performance: complete
date: 2023-01-22 Sunday
---

## Questions

Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sum to `target`.

Each number in `candidates` may only be used **once** in the combination.

**Note:** The solution set must not contain duplicate combinations.

**Example 1:**

```
**Input:** candidates = [10,1,2,7,6,1,5], target = 8
**Output:** 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
```

**Example 2:**

```
**Input:** candidates = [2,5,2,1,2], target = 5
**Output:** 
[
[1,2,2],
[5]
]
```

## Solution

### Backtracking

Standard backtracking question.

```Python
class Solution:

    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        res = []

        candidates.sort() # optimize + pack duplicate
        def backtrack(target, combination, idx):
            if target == 0:
                res.append(list(combination))
            elif target > 0:
                for i in range(idx, len(candidates)):
                    if target - candidates[i] < 0:
                        break # can break early due to sorting

                    # standard method to prevent duplication
                    if i > idx and candidates[i] == candidates[i - 1]:
                        continue

                    combination.append(candidates[i])
                    backtrack(target - candidates[i], combination, i + 1) # i + 1 to not reuse curr element

                    combination.pop()
        backtrack(target=target, combination=[], idx=0)
        return res
```

**Complexity Analysis**
Time: `O(N ^ (T/M + 1))`
Space: `O(T/M)`

---
Link: [[LeetCode]], [[Combination Sum I]]
