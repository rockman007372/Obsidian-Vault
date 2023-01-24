---
tags: LeetCode, leetcode
topics: DP
difficulty: medium
performance: uncomplete
date: 2022-07-30 Saturday
---

## Questions
Input: `int[]` coins and `int` amount
Output: the number of combinations that make up the amount.

Basically, we want all the combinations (unique) of coins, NOT permutations
Eg: 3 = 1 + 2 = 2 + 1 is counted as one combination

## Solution

### Dynamic Programming

Idea: We find the number of combinations that make up the amount between `[0, n]` using EACH coin 

i = 0c
![[Pasted image 20220730170515.png]]

i = 2c
![[Pasted image 20220730170523.png]]

i = 5c
![[Pasted image 20220730170537.png]]

i = 10c
![[Pasted image 20220730170547.png]]
```Java
class Solution {
    public int change(int amount, int[] coins) {
        int[] DP = new int[amount + 1];
        DP[0] = 1;
        
        for (int coin : coins) {
            for (int i = coin; i < amount + 1; i++) {
                if (i >= coin) {
                    DP[i] += DP[i - coin];
                }
            }
        }
        return DP[amount];
    }
}
```

Time: O(C * N) - C is the number of coins, N is amount
Space: O(N)

## Comparison
- This is an extension of [[Coin Change]], which asks for the MINIMUM number of coins to make up an amount.
- This is very similar to [[Combination Sum IV]], but instead of asking for permutations, we are asking for combinations!
	- We can just *switch the for loops order* to get permutations of the amount
	- To understand how the coin loop being outside resolves the double counting, you should pay attention to the fact that when the coin loop is outside, we will count how many combinations are possible with say 2c coin and then add that number to the ways in which the same amount can be created using 3c coin. This imposition of order removes the double counting
	- Compare that with the situation where the coins are in the inner loop. Here we would calculate how many ways we can create an amount using all coins (i.e. 1 and 2 both) and then for the next amount of interest, we will count using all coins (i.e. 1 and 2 both). As you see, we are counting both 1c after 2c and 2c after 1c scenarios, causing the double counting.

---
Tags: [[LeetCode]] - [[Dynamic Programming]]
