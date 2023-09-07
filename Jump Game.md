---
tags: LeetCode
topics: [DynamicProgramming, Greedy]
difficulty: medium
performance: [complete, onTime, notOptimal]
date: 2022-08-01 Monday
---
Tags: [[LeetCode]] - [[Dynamic Programming]] - [[Greedy]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
### My Performance
#complete #onTime #notOptimal 

### Questions
You are given an integer array `nums`. You are initially positioned at the array's **first index**, and each element in the array represents your maximum jump length at that position.

Return `true` _if you can reach the last index, or_ `false` _otherwise_.

**Example 1:**

>**Input:** nums = [2,3,1,1,4]
**Output:** true
**Explanation:** Jump 1 step from index 0 to 1, then 3 steps to the last index.

**Example 2:**

>**Input:** nums = [3,2,1,0,4]
**Output:** false
**Explanation:** You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.

Difficulty: #medium
Input: `int[]` nums
Output: `boolean` can reach destination or not.

### Solution
##### Bottom-Up Dynamic Programming
Idea: 
- We build from the back (right to left).
- `DP[i]` = whether we can reach the end at position i
- Relation: `DP[i]` = true if at least 1 `DP[j]` = true where `i <= j <= i + nums[i]`
![[Pasted image 20220801122256.png]]

Time: O(N^2) - when every index is bad in the worst way (eg: `[3, 2, 1, 0, 1]`)
Space: O(N)

```Java
enum Index {
    GOOD, BAD, UNKNOWN
}

public class Solution {
    public boolean canJump(int[] nums) {
        Index[] memo = new Index[nums.length];
        for (int i = 0; i < memo.length; i++) {
            memo[i] = Index.UNKNOWN;
        }
        memo[memo.length - 1] = Index.GOOD;

        for (int i = nums.length - 2; i >= 0; i--) {
            int furthestJump = Math.min(i + nums[i], nums.length - 1);
            for (int j = i + 1; j <= furthestJump; j++) {
                if (memo[j] == Index.GOOD) {
                    memo[i] = Index.GOOD;
                    break;
                }
            }
        }

        return memo[0] == Index.GOOD;
    }
}
```

My solution (Built from the start) - Almost always O(N^2) since we are checking from left to right:

```Java
class Solution {
    public boolean canJump(int[] nums) {
        int len = nums.length;
        boolean[] dp = new boolean[len];
        dp[0] = true;
        for (int i = 0; i < len; i++) {
            if (dp[i] == false) continue;
            
            int maxJumps = nums[i];
            for (int j = 1; j <= maxJumps && j < len; j++) {
                dp[i + j] = true;
                
                if (i + j == len - 1) return true;
            }
        }
        return dp[len - 1];
    }
}
```

##### Greedy
Idea: 
- Build from the end
- Just have to keep track of the last good index, as long as we can reach that index, we can reach the end.

Time: O(N)
Space: O(1)

```Java
class Solution {
    public boolean canJump(int[] nums) {
        int len = nums.length;
        int lastGoodIndex = len - 1;
        
        for (int i = len - 2; i >= 0; i--) {
            if (i + nums[i] >= lastGoodIndex) {
                lastGoodIndex = i;
            }
        }
        
        return lastGoodIndex == 0;
    }
}
```

Very similar idea based on the fact that we just have to find the nearest index that allow us to cross the '0':
```Java
class Solution {
    public boolean canJump(int[] nums) {
        int len = nums.length;
        if (len == 1) return true;
        
        boolean result = false;
        int lastIndex = 0;
        for (int i = len - 1; i >= 0; i--) {
            if (nums[i] == 0) {
                lastIndex = i;
                result = false;
                
                for (int j = i - 1; j >= 0; j--) {
                    int diff = lastIndex - j;
                    if (diff < nums[j] || (diff == nums[j] && i == len - 1)) {
                        result = true;
                        i = j; // move to the first good index -> allow 1 pass 
                        break;
                    }
                }
                
                // if there is no way to cross the 0
                if (result == false) {
                    return result;
                }
            }
            
            // if current num is positive, continue
        }
        
        return true;
    }
}


/*
Idea: We can only not reach at 0! Must cross the bridge somehow
-> check if we can cross the bridge of 0 is enough!

[0, 5, 0, 1, 0, 4]
          ^
          i = 3
[2, 1, 0, 1, 4]
*/
```