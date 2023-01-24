2022-07-30 21:22
Tags: [[LeetCode]] - [[Dynamic Programming]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# House Robber II
### My Performance
#uncomplete 
### Questions
Difficulty: #medium 
Input: `int[]` representing houses and its money
Output: max amount of money robbed, given 2 consecutive houses cannot be robbed, and all houses at this place are **arranged in a circle**.

eg: `[2, 1, 2]` -> max = 1.

### Solution
- Rob from house 0 to n - 2, then from house 1 to n. Compare.
- Time: O(N)
- Space: O(1)

```Java
class Solution {
    public int rob(int[] nums) {
        int len = nums.length;
        
        if (len == 0) return 0;
        if (len == 1) return nums[0];
        if (len == 2) return Math.max(nums[0], nums[1]);
            
        int first = rob_helper(nums, 0, len - 1);
        int second = rob_helper(nums, 1, len);
            
        return Math.max(first, second);
    }
    
    private int rob_helper(int[] nums, int start, int end) {
        int twoHouses = nums[start];
        int oneHouse = nums[start + 1];
        int temp;
        for (int i = start + 2; i < end; i++) {
            temp = oneHouse;
            oneHouse = Math.max(oneHouse, twoHouses + nums[i]);
            twoHouses = Math.max(temp, twoHouses);
        }
        return Math.max(oneHouse, twoHouses);
    }
}
```