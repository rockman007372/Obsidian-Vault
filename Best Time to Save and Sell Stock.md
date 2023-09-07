---
tags: LeetCode, leetcode
topics: 
difficulty:
performance:
date: 2022-07-24 Sunday
---
---
Link: [[LeetCode]]


## Question

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return _the maximum profit you can achieve from this transaction_. If you cannot achieve any profit, return `0`.

**Example 1:**

>**Input:** prices = [7,1,5,3,6,4]
**Output:** 5
**Explanation:** Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

**Example 2:**

>**Input:** prices = [7,6,4,3,1]
**Output:** 0
**Explanation:** In this case, no transactions are done and the max profit = 0.

## Main Points

### O(N) Space solution 

Idea:
- Make use of [[Maximum Sum Subarray]] 
- Create another array containing the difference btw adjacent elements.
- Find maximum subarray sum -> largest difference

> `[7, 1, 5, 3, 6, 4]`
> `Difference = [-6, 4, -2, 3, -2]`
> `Max Subarray sum = 4 + -2 + 3 = 5 = greatest difference btw 1 and 6`

### Optimal O(1) Space 

+ Maintain 2 variable: minPrice and maxDifference
+ Time: O(n)
+ Space: O(1)
+ Very similar to [[Kadane's Algorithm]], in which we move along the array until we find a more suitable starting point

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # keep track of min element so far
        # keep track of max difference so far
        if not prices:
            return 0

        minPrice = prices[0]
        maxDiff = 0
        for i in range(1, len(prices)):
            curr = prices[i]
            maxDiff = max(maxDiff, curr - minPrice)
            minPrice = min(minPrice, curr)

        return maxDiff
```