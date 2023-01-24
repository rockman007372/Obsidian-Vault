2022-06-05 16:29
Tags: [[Data Structure and Algorithm]]  
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
## When to use
1. Count sth, often the number of ways (Alternatively, use Combinatorics)
2. Minimize/maximize (look for Greedy solution if possible)
3. Yes/no Questions (Greedy if possible)

## Techniques
Can be either iterative (using [[Tabulation]]) or recursive (using [[Memoization]]) 

## Characteristics:
1. Overlapping substructure property:
	+ Use previously calculated results to compute the next result
	+ Can be implemented using [[Memoization]] or [[Tabulation]] technique 
2. Optimal substructure property:
	+ Guarantee an optimal solution to a subproblem can be reused to help you find the optimal solution to a larger problem

## Framework
Example: [[Palindromic Substring]]

1. Define the **DP state** . This is the *result that get reused in further computations*. 
	- DP(i, j) gives a Boolean value stating whether the substring between i<sup>th</sup> and j<sup>th</sup> index is a Palindrome.
	- The answer is the number of DP(i, j) that return true (substrings whose state is true).
2. Identify the base cases. In this question, there are 2 base cases:
	- Single letter substrings are palindromes by definition. i.e. `dp(i, i) = true` ("a")
	- Double letter substrings composed of the same character are palindromes. i.e. ("aa") $$dp(i, i+1) = \begin{cases} true \text { if } S_{i} = S_{i + 1} \\ false \text{ otherwise }  \end{cases}$$
3. Find the **optimal substructure** and hence formulate the **recursive relation**.
	- A string is considered a palindrome if:
		- Its first and last characters are equal
		- The body of the string is also a palindrome
	- Recurrence relation: $$dp(i, j) = \begin{cases} true \text { if } s_{i}= s_{j} \text { and } dp(i + 1, j - 1) \\ false \text { otherwise }\end{cases}$$
4. Identify **overlapping subproblems** and compute them once.

## Example
### Fibonacci
```
F[0] = 0, F[1] = 1
F[i] = F[i - 1] + F[i - 2]
```
We can a solve recursively with [[Memoization]] technique to reduce runtime from O(2^N) to O(N)

Time: O(N)
Space: O(N)

```Java
public class Fibonacci {
    public static int fib(int n, int[] memoized) {
        if (n <= 0) return 0;
        if (n == 1) return 1;
        if (memoized[n] != 0) return memoized[n];
        int result = fib(n - 1, memoized) + fib(n - 2, memoized);
        memoized[n] = result;
        return result;
    }
    
    public static void main(String[] args) {
        System.out.println(Fibonacci.fib(41, new int[101]));
    }
}
```

Or we can solve iteratively using the first 2 numbers to build the next number (overlapping substructure). The order in iterative DP is very important. In this case, we just need to keep track of 2 previous number at every state.

Time: O(N) ; Space: O(1)

```Java
public class FibIter {    
    public static int fib(int n) {
	    int fib = 0;
	    int next = 1;
	    for (int i = 0; i < n; i++) {
		    int temp = next;
		    next += fib;
		    fib = temp;
	    }
	    return fib;
    }
    
    public static void main(String[] args) {
        System.out.println(fib(10));
    }
}
```


### Counting Stairs
See [[Counting Stairs]].

### Minimum Path Sum 
Check [[Minimum Path Sum]] for more details.
Given a 2D array grid, find the minimum sum from top left to bottom right. **You can only move down or right.**

>`DP[row][column] = min(DP[row - 1][column], DP[row][column - 1]) + arr[row][column]