2022-06-05 16:44
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Best Time to Save and Sell Stock
#easy 

### Question
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

### Main Points
##### O(N) Space solution using [[Maximum Sum Subarray]] 
Idea:
- Create another array containing the difference btw adjacent elements.
- Find maximum subarray sum -> largest difference

> `[7, 1, 5, 3, 6, 4]`
> `Difference = [-6, 4, -2, 3, -2]`
> `Max Subarray sum = 4 + -2 + 3 = 5 = greatest difference btw 1 and 6`

##### Optimal O(1) Space 
+ Maintain 2 variable: minPrice and maxDifference
+ Time: O(n)
+ Space: O(1)
+ Very similar to [[Kadane's Algorithm]], in which we move along the array until we find a more suitable starting point

``` Java 
class Solution {
    public int maxProfit(int[] prices) {
        int minPrice = prices[0];
        int maxDifference = 0;
        for (int i = 0; i < prices.length; i++) {
            // start from the next minimum price 
            if (prices[i] < minPrice) {
                minPrice = prices[i];
            }
            
            // else, we find the max profit so far
            if (prices[i] - minPrice > maxDifference) {
                maxDifference = prices[i] - minPrice;
            }
        }
        
        return maxDifference;
    }
}
```

More resemblance to Kadane's:
```Java
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length == 0){
            return 0;
        }
        int profit = 0;
        int buy = prices[0];
        for(int i=1; i<prices.length; i++){
            buy = Math.min(buy,prices[i]);
            profit = Math.max(profit,prices[i]-buy);
        }
        return profit;
    }
```