---
tags: LeetCode, leetcode
topics: dp, memoization, recursion
difficulty: hard
performance: uncomplete
date: 2023-07-23 Sunday
---

## Questions

Given an input string `s` and a pattern `p`, implement regular expression matching with support for `'.'` and `'*'` where:

- `'.'` Matches any single character.​​​​
- `'*'` Matches zero or more of the preceding element.

The matching should cover the **entire** input string (not partial).

## Solution

Recognize that this problem has 2 DP properties:
- Optimal Substructure: `s = abc` and `p = a*b*c`.  If we know `bc` matches `*b*c`, we just need to check if `a` matches
- Overlapping Substructure: Harder to see that some problems are recurrent, unless we come up with a recursive relation first.

Recursive solution idea:
- If the next letter of p is a `*`, you have 2 cases:
	- Skip the letter `*` and move on to the next letter of p
	- Check if the current letter of s matches the current letter of p, then move on to the next letter of s
- Else, simply check if the first letter of s and p matches, move on to the next letter of both strings.

### Memoization

```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        sLen = len(s)
        pLen = len(p)

        @cache
        def helper(i: int, j: int):
            # if pattern is empty, check if string is empty
            if j == pLen:
                return i == sLen 

            firstMatch = (i != sLen) and (p[j] in {s[i], '.'})
            
            if j + 1 != pLen and p[j + 1] == '*':
                return helper(i, j + 2) or \
                    (firstMatch and helper(i + 1, j))

            return firstMatch and helper(i + 1, j + 1)

        return helper(0, 0)
```

Time and space: O(SP). We only compute the result of each dp(s, p) once. 

### DP

```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        dp = [[False for _ in range(len(p) + 1)] for _ in range(len(s) + 1)]
        dp[len(s)][len(p)] = True

        for i in range(len(s), -1, -1):
            for j in range(len(p) - 1, -1, -1):
                
                firstMatch = (i < len(s)) and (p[j] in {s[i], '.'})
                if j + 1 < len(p) and p[j + 1] == '*':
                    dp[i][j] = dp[i][j + 2] or (firstMatch and dp[i + 1][j])
                else:
                    dp[i][j] = firstMatch and dp[i + 1][j + 1]
        
        return dp[0][0]
```

---
Link: [[LeetCode]]
