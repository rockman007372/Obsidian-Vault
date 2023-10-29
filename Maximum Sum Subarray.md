---
tags:
  - LeetCode
  - leetcode
topics: 
difficulty: medium
performance: uncompleted
date: 2022-07-24 Sunday
---
## Question

Given an array of numbers, return the maximum sum of a contiguous subarray of any size.

## Solution

+ Technique: [[Dynamic Programming]]
+ Can be solved efficiently with [[Kadane's Algorithm]] with O(1) space
+ See also: [[Longest Increasing Subsequence]]
+ Time: O(n)
+ Space: O(n)

### Dynamic Programming

``` Java 
class Solution {
    public int maxSubArray(int[] nums) {
	    // use tabulation to create array subArray where 
	    // subArray[i] = greatest subarray sum starting at i
        int len = nums.length;
        int[] subArray = new int[len];
        subArray[len - 1] = nums[len - 1];
        for (int i = len - 2; i >= 0; i--) {
            if (nums[i] + subArray[i + 1] < nums[i]) {
                subArray[i] = nums[i]; // DP
            } else {
                subArray[i] = nums[i] + subArray[i + 1];
            }
        }
        
	    // Iterate through tabulation table to find max
        int max = Integer.MIN_VALUE;
        for (int i = 0; i < subArray.length; i++) {
            if (subArray[i] > max) {
                max = subArray[i];
            }
        }
        return max;
    }
}
```

### Kadane's Algorithm

Key idea: If current sum is ever negative, discard it (because you will only end up with a loss if you include the prior sum)

``` Java
class Solution {
    public int maxSubArray(int[] nums) {
        // Initialize our variables using the first element.
        int currentSubarray = nums[0];
        int maxSubarray = nums[0];
        
        // Start with the 2nd element since we already used the first one.
        for (int i = 1; i < nums.length; i++) {
            int num = nums[i];
            // If current_subarray becomes less than the current num,
            // throw it away. Otherwise, keep adding to it.
            currentSubarray = Math.max(num, currentSubarray + num);
            maxSubarray = Math.max(maxSubarray, currentSubarray);
        }
        
        return maxSubarray;
    }
}
```

```
def getMaxProfit(pnl, k):

    # Solution 1: DP

    # # Write your code here

    # n = len(pnl)

    # dp = [0 for _ in range(n)]

    # res = 0

    # # possible subset size

    # for j in range(1, k + 1):

    #     for i in range(n - j + 1):

    #         dp[i] = dp[i] + pnl[i + j - 1]

    #         res = max(res, dp[i])

    # return res

    # Solution 2: Prefix Sum O(nk)

    n = len(pnl)

    prefixSum = [0] * n

    prefixSum[0] = pnl[0]

    for i in range(1, n):

        prefixSum[i] = pnl[i] + prefixSum[i - 1]

    res = 0

    for j in range(1, k + 1):

        for i in range(n - j + 1):

            curr = 0

            if i - 1 >= 0:

                curr = prefixSum[i + j - 1] - prefixSum[i - 1]

            else:

                curr = prefixSum[i + j - 1]

            res = max(res, curr)

    return res
```