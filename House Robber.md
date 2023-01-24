2022-07-30 16:14
Tags: [[LeetCode]] - [[Dynamic Programming]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
See also: [[House Robber II]]

### My Performance
#complete #notOptimal 

### Questions
Difficulty: #medium 
Input: `int[]` representing money in house i
Output: max amount of money robbed, given 2 consecutive houses cannot be robbed

### Solution
##### Optimize Dynamic Programming

```
DP[i] = max money from 0 to i (may or may not be inclusive of house i)
DP[i] = max(DP[i - 1] , DP[i - 2] + nums[i])
DP[0] = nums[0]
DP[1] = nums[1]
```

Time: O(N)
Space: O(1)

```Java
class Solution {
    public int rob(int[] nums) {
        int n = nums.length;
        if (n == 0) return 0;
        if (n == 1) return nums[0];
        
        int twoHouse = nums[0];
        int oneHouse = nums[1];
        for (int i = 2; i < n; i++) {
            int temp = oneHouse;
            oneHouse = Math.max(twoHouse + nums[i], oneHouse);
            twoHouse = Math.max(temp, twoHouse);
        }
        
        return Math.max(oneHouse, twoHouse);
    }
}

/*
2, 1, 1, 2
      ^

two = 2
one = 3
temp = 1


[2, 3, 0, 1000, 2000] -> 2003

DP = [2, 3, 3, 1003, 2003]
max = 2003

input: array of numbers representing money in the house
output: max amt of money, given that cannot rob 2 houses in a row

example: 
[1, 2, 3 , 4]

max = 6
DP[i] = max money from 0 to i (may or may not be inclusive of house i)
DP[i] = max(DP[i - 1] , DP[i - 2] + nums[i])
DP[0] = nums[0]
DP[1] = nums[1]

[1, 2, 3, 4]
DP = [1, 2, 4, 6]

Time = O(N) = 1 + 2 + 3 + 4...N
Space = O(1)
*/
```