---
tags: LeetCode, leetcode
topics: dp, greedy
difficulty: medium
performance: uncomplete
date: 2023-06-28 Wednesday
---

## Questions

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day, and an integer `fee` representing a transaction fee.

Find the maximum profit you can achieve. You may complete as many transactions as you like, but you need to pay the transaction fee for each transaction.

**Note:**
- You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).
- ! The transaction fee is only charged once for each stock purchase and sale. It is charged at the time you sell the stock.

## Solution

### DP 

```python
'''
at day i, you either hold a stock or alr sold the stock.
        
hold[i]
= best profit if you hold a stock at day i 
= either do nothing if you alr hold a stock OR buy a new stock if you have not hold any stock
= max(hold[i - 1], free[i - 1] - prices[i])
        
free[i]
= best profit if you did not hold any stock at day i 
= either do nothing if u do not hold any stock or sell the stock at day i's price
= max(free[i - 1], hold[i - 1] + price[i] - fee)
'''
```

>[!key point]
> Dont think of the difference between the stocks I bought previously and the stock I sell today, but think of stocks as a culmination of buying and selling at different point. 

```python
class Solution:
    def maxProfit(self, prices: List[int], fee: int) -> int:
        
        n = len(prices)
        hold = [0] * n
        free = [0] * n
        
        # on the first day
        hold[0] = -prices[0] # bought stock on the first day
        free[0] = 0          # did not by any stock
        
        # on subsequent days
        for i in range(1, n):
            hold[i] = max(hold[i - 1], free[i - 1] - prices[i])
            free[i] = max(free[i - 1], hold[i - 1] + prices[i] - fee)
        
        return max(hold[n - 1], free[n - 1])
```

Space and Time: O(N)

### Greedy

You only need the 2 cases of maximum profit of previous day.

```python
class Solution:
    def maxProfit(self, prices: List[int], fee: int) -> int:
        n = len(prices)

        # on the first day
        hold = -prices[0]
        free = 0

        # on subsequent days
        for i in range(1, n):
            temp = hold
            hold = max(hold, free - prices[i])
            free = max(free, temp + prices[i] - fee)

        return max(hold, free)
```



---
Link: [[LeetCode]]
