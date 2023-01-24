2022-07-15 11:29
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

### My Performance
#complete #onTime 

### Questions
Difficulty: #easy 
Count the number of ways to climb stairs if you can either climb 1 or 2 stairs.

### Solution

##### Bottom-Up Approach with [[Dynamic Programming]]
- State: `DP[i]` = number of ways to climb i stairs by climbing either 1 or 2 stairs at once. 
- Recursive relation: `DP[i] = DP[i - 1] + DP[i - 2]`, where DP[i] is the number of ways to climb to that stair.
- We can just keep track of 2 variables similar to Fibonacci.
  
```Java
class Solution {
	public int climbStairs(int n) {
		if (n < 0) return 0;
		int downOne = 1;
		int downTwo = 1;
		for (int i = 2; i <= n; i++) {
			int temp = downOne;
			downOne += downTwo;
			downTwo = temp;
		}
		return downOne;
	}
}
```

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        curr = 0
        next = 1

        for i in range(n):
            next, curr = next + curr, next

        return next

"""

1. DP solution:
- state: DP(n) = number of way to reach step n
- Relation: DP(n) = DP(n - 1) + DP(n - 2)
- Time: O(N)
- Space: O(N)

2. Constant Space sol - Fibonanci
- notice that the next state depends on 2 previous state

Testing:
curr = 0, next = 1
i = 0: curr = 1, next = 1 → n = 1
i = 1: curr = 1, next = 2 → n = 2
"""
```

##### Top-Down Approach with [[Memoization]]
```Java
class Solution {
    public int climbStairs(int n) {
        return climbHelper(n, new int[n + 1]);
    }
    
    public int climbHelper(int n, int[] memoize) {
        if (n < 0) return 0;
        if (n <= 1) return 1;
        if (memoize[n] != 0) return memoize[n];
        int result = climbHelper(n - 1, memoize) + climbHelper(n - 2, memoize);
        memoize[n] = result;
        return result;
    }
}
```