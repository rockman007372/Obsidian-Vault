---
tags: LeetCode
aliases: 
topics: backtracking
difficulty: medium
performance: uncomplete
---
Date:: 2022-08-13 Saturday 
Link: [[LeetCode]] - [[Backtracking]]
- - -

## Questions
Input: `int[] nums`
Output: a list of all permutations of the nums. There are **no duplicates** in `nums`. Contrast this with [[Permutation II]]

## Solution
### Backtracking
![[Permutation 2022-07-14 15.13.32.excalidraw]]

Time: O(N!) 

Space: O(N * N!) - N! lists of size N 
If we do not count output space: O(N) - recursion stack

```Java
class Solution {
    private List<List<Integer>> res = new ArrayList<>();
    
    public List<List<Integer>> permute(int[] nums) {
        // create an arraylist of the nums array
        ArrayList<Integer> numsList = new ArrayList<>();
        for (int num : nums) {
            numsList.add(num);
        }
        
        backtrack(numsList, 0);
        
        return res;
    }
    
    // permute by backtracking: choose a digit to be the start, 
    // permute the remaining digits, add permutation to the res list,
    // then backtrack and choose a new digit to be the start
    private void backtrack(ArrayList<Integer> numsList, int idx) {
        if (idx == numsList.size() - 1) {
            res.add(new ArrayList<Integer>(numsList));
        } else {
            for (int i = idx, n = numsList.size(); i < n; i++) {
                Collections.swap(numsList, idx, i);
                backtrack(numsList, idx + 1);
                Collections.swap(numsList, idx, i);
            }
        }
        
    }
}
