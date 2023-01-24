2022-06-05 16:44
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
### Main Points
+ [[Dynamic Programming]]
+ Break down the problems into smaller subproblems:
	+ All positive numbers: Just find the largest product streak
	+ If there is a 0: streak is reset to the next element
	+ if there is a negative number: product becomes minimum, can become maximum again if another negative number is seen, unless we meet a 0 when the streak is reset.
+ Keep track of **max product so far** and **min product so far** (in case we encounter a negative number later)
![[Pasted image 20220606172649.png]]
+ Code: 
  
``` Java
  class Solution {
    public int maxProduct(int[] nums) {
        if (nums.length == 0) return 0;

        int max_so_far = nums[0];
        int min_so_far = nums[0];
        int result = max_so_far;

        for (int i = 1; i < nums.length; i++) {
            int curr = nums[i];
            int temp_max = Math.max(curr, Math.max(max_so_far * curr, min_so_far * curr));
            min_so_far = Math.min(curr, Math.min(max_so_far * curr, min_so_far * curr));

            max_so_far = temp_max;

            result = Math.max(max_so_far, result);
        }

        return result;
    }
}
``` 