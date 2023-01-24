---
tags: LeetCode, leetcode
topics: backtracking
difficulty: medium
performance: complete
date: 2023-01-22 Sunday
---

## Questions



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
