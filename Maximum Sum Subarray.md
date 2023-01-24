2022-06-05 16:44
Tags: [[LeetCode]] 
- - -
### Main Points
+ Technique: [[Dynamic Programming]]
+ Can be solved efficiently with [[Kadane's Algorithm]] with O(1) space
+ See also: [[Longest Increasing Subsequence]]
+ Time: O(n)
+ Space: O(n)

##### Dynamic Programming
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

##### Kadane's Algorithm

Key idea: If current sum is ever negative, discard it. 

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