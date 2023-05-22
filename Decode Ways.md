---
tags: LeetCode
topics: DynamicProgramming
difficulty: medium
performance: [complete, notOnTime, notOptimal]
date: 2022-07-31 Sunday
---

## Questions
A message containing letters from `A-Z` can be **encoded** into numbers using the following mapping:

>'A' -> "1"
>'B' -> "2"
>...
>'Z' -> "26"

To **decode** an encoded message, all the digits must be grouped then mapped back into letters using the reverse of the mapping above (there may be multiple ways). For example, `"11106"` can be mapped into:

-   `"AAJF"` with the grouping `(1 1 10 6)`
-   `"KJF"` with the grouping `(11 10 6)`

Note that the grouping `(1 11 06)` is invalid because `"06"` cannot be mapped into `'F'` since `"6"` is different from `"06"`.

Given a string `s` containing only digits, return _the **number** of ways to **decode** it_.

Difficulty: #medium 
Input: `String` s reprenting code
Output: `int` number of ways to decode it

## Solution
##### Dynamic Programming
State: `DP[i]` = no. ways to decode from 0 to i
Recursive relation: `DP[i] = DP[i - 2] + DP[i - 1] if valid combi and S[i] != 0`
Time: O(N)
Space: O(N)

```Java
class Solution {
    public int numDecodings(String s) {
        int len = s.length();
        if (len == 0) return 0;
        if (s.charAt(0) == '0') return 0;
        
        int[] DP = new int[len + 1]; // offset by 1
        DP[0] = 1; // offset
        DP[1] = 1; // first char cannot be 0 at this point
            
        for (int i = 2; i <= len; i++) {
            if (s.charAt(i - 1) != '0') {
                DP[i] = DP[i - 1];
            } 
            
            // substring btw i - 2 and i - 1
            int doubleDigit = Integer.valueOf(s.substring(i - 2, i)); 
            if (doubleDigit >= 10 && doubleDigit <= 26) {
                DP[i] += DP[i - 2];
            }
        }
        
        return DP[len];
    }
}
```

```Java
// My shittyass solution -> SHOULD HAVE COME UP WITH RECURSIVE RELATION PROPERLY FIRST
class Solution {
    public int numDecodings(String s) {
        int len = s.length();
        if (len == 0) return 0;
        if (s.charAt(0) == '0') return 0;
        
        int[] DP = new int[len];
        DP[0] = 1;
            
        for (int i = 1; i < len; i++) {
		    // get double digits
            int prev = s.charAt(i - 1) - '0';
            int curr = s.charAt(i) - '0';
            int sum = prev * 10 + curr;  
            
            if (prev != 0 && sum <= 26) {
                DP[i] = (i != 1) 
                    ? DP[i - 2]
                    : 1;
            } 
            
            if (curr != 0) {
                DP[i] += DP[i - 1];
            } else {
                DP[i - 1]--; // bad practice, cannot modify previous optimal result 
            }
        }
        return DP[len - 1];
    }
}

/*
   v
"11106"
     ^
DP = [1, 2, 2, 2, 2]
i = 2

ANS: 2
> 1, 1, 10, 6
> 11, 10, 6
*/
```

##### Optimized DP - Constant Space

```Java
class Solution {
    public int numDecodings(String s) {
        int len = s.length();
        if (len == 0) return 0;
        if (s.charAt(0) == '0') return 0;
        
        int prev = 1; // offset
        int curr = 1; // first char cannot be 0 at this point
        int temp = 0;
        
        for (int i = 2; i <= len; i++) {
            temp = curr;
            if (s.charAt(i - 1) == '0') {
                curr = 0;
            } 
            
            // substring btw i - 2 and i - 1
            int doubleDigit = Integer.valueOf(s.substring(i - 2, i)); 
            if (doubleDigit >= 10 && doubleDigit <= 26) {
                curr += prev;
            }
            
            prev = temp;
        }
        
        return curr;
    }
}
```