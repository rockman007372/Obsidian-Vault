2022-06-05 16:44
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

## Questions
Input: `int[]` cost, where `cost[i]` is the cost to climb to another step from` step[i]`. You can either take 1 step or 2 step at one time.

Output: Minimum cost to reach the last step (step n + 1 <sup>th</sup>)

```
[1, 2, 3, 4, 5] → (2, 4) = 6
```

## Solution
##### [[Dynamic Programming]] (Bottom-up approach)
Time and Space: O(n)
- State: DP[i] = min cost to reach i<sup>th</sup> step
- Recursive relation: (Either take 1 step or 2 step)
```
DP[i] = Math.min(DP[i - 1] + cost[i - 1], DP[i - 2] + cost[i - 2])
``` 

##### DP with constant space
Just like [[Fibonacci]] sequence, only need to keep track of the previous 2 steps
Space: O(1)

```Java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int downOne = 0;
        int downTwo = 0;
        for (int i = 2; i < cost.length + 1; i++) {
            int temp = downOne;
            downOne = Math.min(downOne + cost[i - 1],
	            downTwo + cost[i - 2]);
            downTwo = temp;
        }
        
        return downOne;
    }
}
```

##### Recursion with [[Memoization]] (Top Down)
Use a HashMap instead of array for good practice, because there will often be multiple arguments, non-integer arguments,...
Time and Space: O(n)

```Java
class Solution {
    private HashMap<Integer, Integer> memo = new HashMap<Integer, Integer>();

    public int minCostClimbingStairs(int[] cost) {
        return minimumCost(cost.length, cost);
    }

    private int minimumCost(int i, int[] cost) {
        // Base case, we are allowed to start at either step 0 or step 1
        if (i <= 1) {
            return 0;
        }

        // Check if we have already calculated minimumCost(i)
        if (memo.containsKey(i)) {
            return memo.get(i);
        }

        // If not, cache the result in our hash map and return it
        int downOne = cost[i - 1] + minimumCost(i - 1, cost);
        int downTwo = cost[i - 2] + minimumCost(i - 2, cost);
        memo.put(i, Math.min(downOne, downTwo));
        return memo.get(i);
    }
}
```