---
tags: LeetCode, leetcode
topics: backtracking, recursion
difficulty: medium
performance: uncomplete
date: 2022-07-27 Wednesday
---

## Questions

Input: `int[] candidates` and `int target` 
Output: list of **unique** combinations summing up to `target`

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.


```
Input: candidates = `[2,3,6,7]`, target = 7
Output: `[[2,2,3],[7]]`

Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.
(2 + 2 + 3) and and (3 + 2 + 2) are considered the same.
```

Assumptions:
- All the elements in `nums` are **unique**
- Compare this to [[Subsets II]], which allows duplicates in `nums`

## Solution
### Backtracking


```Java
class Solution {
    private List<List<Integer>> res;
    
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        res = new ArrayList<>();
        Arrays.sort(candidates); // minor optimization to prune tree
        helper(new ArrayList<Integer>(), candidates, target, 0);
        return res;
    }
    
    private void helper(ArrayList<Integer> curr, int[] candidates, int target, int start) {
        // if (target < 0) return;
        
        if (target == 0) {
            res.add(new ArrayList<>(curr));
            return;
        }
        
        for (int i = start; i < candidates.length; i++) {
            int candidate = candidates[i];
            if (target < candidate) break; // prune search
            
            curr.add(candidate);
            helper(curr, candidates, target - candidate, i); 
            // start variable prevents duplication of lists
            // eg: {1, 2, 2} and {2, 1, 2} 
            curr.remove(curr.size() - 1);
        }
    }
}
```


**Python solution with optimization:**
The solution can be optimized a little by (1) sort the candidates array and (2) exit the loop in recursive call earlier when we are sure adding the rest of the elements will be over the target

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        
        res = []

        candidates.sort() # optimize to prune tree earlier

        def backtrack(target, combination, idx):

            if target == 0:
                res.append(list(combination))
            elif target > 0:
                for i in range(idx, len(candidates)):

                    if target - candidates[i] < 0:
                        break # can break early due to sorting
                        
                    combination.append(candidates[i])
                    backtrack(target - candidates[i], combination, i)
                    combination.pop()
    

        backtrack(target=target, combination=[], idx=0)
        return res
```

**Complexity Analysis**

Time: O($N^{\frac{T}{M} + 1}$) 
- N is the number of candidates, T is the target, M is the smallest candidate
- ! Runtime = number of nodes in N-ary tree
- Branch-out factor of each node is N
- The maximal depth of the tree is $\frac{T}{M}$, where we keep adding the smallest elements until target is reached.
- Maximal number of nodes = O($N^{\frac{T}{M} + 1}$) → O(1 + 2 + 4 + ... + N^T/M)

![[Combination Sum I 2022-07-27 18.22.37.excalidraw]]

Space: O($\frac{T}{M}$) 
- Recursion stack is the depth of the tree

---
Tags: [[LeetCode]] - [[Backtracking]]
