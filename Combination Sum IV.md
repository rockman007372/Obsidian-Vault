---
tags: LeetCode, leetcode
topics: backtracking, DP
difficulty: medium
performance: complete
date: 2022-07-27 Wednesday
---

## Questions

Input: `int[]` nums and `int` target
Output: Number of PERMUTATIONS that make up a target (eg. {1, 2} and {2, 1} are 2 different permutations).

**Example 1:**

```
**Input:** nums = [1,2,3], target = 4
**Output:** 7
**Explanation:**
The possible combination ways are:
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)
Note that different sequences are counted as different combinations.
```

**Example 2:**

```
**Input:** nums = [9], target = 3
**Output:** 0
```

## Comparsion
- This is an extension of [[Combination Sum I]], which asks for the list of all unique combinations that make up a target.
- Very similar to [[Coin Change II]], but we are asking for permutation, not combination.
- By _switching the order of loops_ in one of the solutions of [[Coin Change II]], one could solve this problem.

## My Performance
#complete #onTime 

## Solution
### Dynamic Programming
Time: O(N * L) - N = target, L = length of nums 
Space: O(N)

```Java
class Solution {
    public int combinationSum4(int[] nums, int target) {
        Arrays.sort(nums); // minor optimization
        int[] DP = new int[target + 1];
        DP[0] = 1;
        for (int i = 1; i < target + 1; i++) {
            for (int j = 0; j < nums.length; j++) {
                int remains = i - nums[j];
                if (remains >= 0) {
                    DP[i] += DP[remains];
                } else {
                    break; // eary stopping
                }
            }
        }
        return DP[target];
    }
}
```

```python
class Solution:
    def combinationSum4(self, nums: List[int], target: int) -> int:
        
        """ 
        DP solution
        1. DP[i] = number of permutation whose sum is i
        2. DP[i] += DP[i - num] for num in nums
        """

        DP = [0] * (target + 1)
        DP[0] = 1 # to increment the sum

        nums.sort() # to prune the search early

        for sum in range(1, target + 1):
            for num in nums:
                if sum - num < 0:
                    break

                DP[sum] += (DP[sum - num])            

        return DP[target]
```

### Top-Down Memoization
```Java
class Solution {
    private HashMap<Integer, Integer> memo;

    public int combinationSum4(int[] nums, int target) {
        // minor optimization
        // Arrays.sort(nums);
        memo = new HashMap<>();
        return combs(nums, target);
    }

    private int combs(int[] nums, int remain) {
        if (remain == 0)
            return 1;
        if (memo.containsKey(remain))
            return memo.get(remain);

        int result = 0;
        for (int num : nums) {
            if (remain - num >= 0)
                result += combs(nums, remain - num);
            // minor optimizaton, early stopping
            // else
            //     break;
        }
        memo.put(remain, result);
        return result;
    }
}
```

- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
Tags: [[LeetCode]] - [[Coin Change]] - [[Dynamic Programming]]

