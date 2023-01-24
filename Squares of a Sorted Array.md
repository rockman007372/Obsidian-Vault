2022-06-05 16:44
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Squares of a Sorted Array
### Questions
Input: Sorted nums array
Output: Sorted **squared** nums array

Eg: 
```
nums = [-3, -2, -1, 1, 2, 3]
output = [1, 1, 4, 4, 9, 9]
```

### Solution
Use 2 pointers at beginning and end, then follow Merge step in [[Merge Sort]].

```Java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int lo = 0; int hi = nums.length - 1;
	    int[] res = new int[nums.length];
	    int index = nums.length - 1;
	    while (lo <= hi) {
		    if (Math.abs(nums[lo]) >= Math.abs(nums[hi])) {
			    res[index--] = (int) Math.pow(nums[lo], 2);
			    lo++;
		    } else {
			    res[index--] = (int) Math.pow(nums[hi], 2);
			    hi--;
		    }
	    }
	    return res;
    }
}
```
Time: O(n)
Space: O(n) if output is taken into account