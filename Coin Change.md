---
tags: LeetCode, leetcode
topics: DP, memoization
difficulty: medium
performance: uncomplete
date: 2022-07-24 Sunday
---

## Questions
Input: coins denomination `int[]`, `int` amount
Output: min number of coins required to make up amount, given unlimited coins

## Solution
### Bottom-Up [[Dynamic Programming]]
- State: `DP[S]` = Min number of ways to make up S amount.
- Relation: `DP[S] = Min(DP[S - ci]) + 1` for i = 0, 1, ..., n - 1, subject to `S - ci >= 0`
- Time: O(S * n) - S is amount and n is number of coins
- Space: O(S) - tabulation table

```Java
class Solution {
    public int coinChange(int[] coins, int amount) {
        if (amount == 0) return 0;
        if (amount < 0 || coins.length == 0) return -1;
        
        int[] DP = new int[amount + 1];
        Arrays.fill(DP, amount + 1); // coin denomination is >= 1, 
        // hence min coin change cant be greater than amount.
        
        DP[0] = 0;
        for (int S = 1; S <= amount; S++) {
            for (int c = 0, n = coins.length; c < n; c++) {
                if (S - coins[c] >= 0) {
                    DP[S] = Math.min(DP[S], DP[S - coins[c]] + 1);
                }
            }
        }
        
        return DP[amount] == amount + 1 ? -1 : DP[amount];
    }
}
```

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        """
        DP[i] = min number of coins to make up i amount
        DP[i] = min(DP[i - coin]) + 1 for coin in coins
        """

        if amount <= 0:
            return 0
            
        DP = [float('inf')] * (amount + 1)
        DP[0] = 0
        
        for sum in range(amount + 1):
            for coin in coins:
                if sum - coin >= 0:
                    DP[sum] = min(DP[sum - coin] + 1, DP[sum])
                    
        return DP[amount] if DP[amount] != float('inf') else -1
```


### Top-Down [[Memoization]]

```Java
public class Solution {

  public int coinChange(int[] coins, int amount) {
    if (amount < 1) return 0;
    cache = new int[amount];
    return coinChange(coins, amount);
  }

  private int[] cache;
  private int coinChange(int[] coins, int rem) {
    if (rem < 0) return -1;
    if (rem == 0) return 0;
    if (cache[rem - 1] != 0) return cache[rem - 1]; // if memoized, just read
    
    int min = Integer.MAX_VALUE;
    for (int coin : coins) {
      int res = coinChange(coins, rem - coin);
      if (res >= 0 && res < min) // only update if condition passes
        min = 1 + res;
    }
    
    count[rem - 1] = (min == Integer.MAX_VALUE) ? -1 : min; // memoization
    return count[rem - 1];
  }
}
```

### Approach similar to CS1101S
```Java
class Solution {
    private int[][] cache;
    public int coinChange(int[] coins, int amount) {
        cache = new int[coins.length][amount + 1];
        return coinHelper(coins, 0, amount);
    }
    
    private int coinHelper(int[] coins, int idx, int amount) {
        if (amount == 0) return 0;
        if (amount < 0 || idx >= coins.length) return -1;
        
        if (cache[idx][amount] != 0) return cache[idx][amount];
        
        int head = coins[idx];
        int withoutHead = coinHelper(coins, idx + 1, amount);
        int withHead = coinHelper(coins, idx, amount - head) + 1;
        
        if (withoutHead <= 0 && withHead <= 0) {
            cache[idx][amount] = -1;
            return -1;
        } else if (withoutHead <= 0) {
            cache[idx][amount] = withHead;
            return withHead;
        } else if (withHead <= 0) {
            cache[idx][amount] = withoutHead;
            return withoutHead;
        } else {
            cache[idx][amount] = Math.min(withHead, withoutHead);
            return cache[idx][amount];
        }
    }
}

/*

Wrong Approach:
1. sort the coins in decreasing order
2. keep adding up the largest coin until we exceed the amount, then we minus the largest coin once, then we continue adding the next largest coin
3. we stop when we amount = 0; 
4. if amount is never 0, we return -1 -> we cannot make up the amount from the coins we have
=> Wrong, because there may still be ways to make up amount using smaller coins!

DP approach:
We find all combinations of coin change and iterate through to see which one is smallest
We can either use the first coin or not, hence we have the recursion relation:

coinChange(coins, amount) = min(
	coinChange(coins.removeHead(), amount), 
	coinChange(coins, amount - head) + 1
)

*/
```

---
Link: [[LeetCode]], [[Dynamic Programming]], [[Recursion]], [[Coin Change II]]
