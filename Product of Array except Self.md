2022-06-05 16:44
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Product of Array except Self
Given an integer array `nums`, return _an array_ `answer` _such that_ `answer[i]` _is equal to the product of all the elements of_ `nums` _except_ `nums[i]`.

### Main Points
- Make use of [[Prefix Sum]]
- Idea: 
	- Build left prefix product array and right prefix product array
	- Multiply each pair of entries

```
[2, 3, 1, 4]

left_prefix_product = [1, 2, 6, 6]
right_prefix_product = [12, 4, 4, 1]
result = [12, 8, 24, 6]
```
  
- Time: O(n)
- Space: O(1) or O(n) if counting new array

``` Java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int[] result = new int[nums.length]; 
        
        // build left prefix product
        result[0] = 1;
        for (int i = 1; i < nums.length; i++) {
             result[i] = result[i - 1] * nums[i - 1]; 
        }
         
        int prefixRight = 1;
        for (int i = nums.length - 1; i >= 0; i--) {
            result[i] = result[i] * prefixRight;
            prefixRight *= nums[i];
        }
        return result;
    }
}
```