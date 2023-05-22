---
tags: LeetCode, leetcode
topics: dp
difficulty: medium
performance: complete
date: 2023-05-13 Saturday
---

## Questions

Given the integers `zero`, `one`, `low`, and `high`, we can construct a string by starting with an empty string, and then at each step perform either of the following:

-   Append the character `'0'` `zero` times.
-   Append the character `'1'` `one` times.

This can be performed any number of times.

A **good** string is a string constructed by the above process having a **length** between `low` and `high` (**inclusive**).

Return _the number of **different** good strings that can be constructed satisfying these properties._ Since the answer can be large, return it **modulo** `109 + 7`.

**Example 1:**

**Input:** low = 3, high = 3, zero = 1, one = 1
**Output:** 8
**Explanation:** 
One possible valid good string is "011". 
It can be constructed as follows: "" -> "0" -> "01" -> "011". 
All binary strings from "000" to "111" are good strings in this example.

**Example 2:**

**Input:** low = 2, high = 3, zero = 1, one = 2
**Output:** 5
**Explanation:** The good strings are "00", "11", "000", "110", and "011".

## Solution

Time: O(N)
Space: O(N) where N = high

```python
class Solution:
    def countGoodStrings(self, low: int, high: int, zero: int, one: int) -> int:
        dp = [0] * (high + 1)
        dp[0] = 1
        
        for i in range(high + 1):
            if i >= zero:
                dp[i] += dp[i - zero]
            if i >= one:
                dp[i] += dp[i - one]

        return sum(dp[low : high + 1]) % (pow(10,9) + 7)
        
'''

dp[i] = number of combinations with i characters 
dp[i] = dp[i - zero] + dp[i - one] 

what if i < zero or i < one! must take into account


inputs: low, hi, zero, one
output: the max number of strings satisfying these conditions:

1. lo <= string.length <= hi
2. at each step, i can append "zero" zeros or "one" ones


example 1:
lo = 5, hi = 5
zero = 1
one = 1
combinations: 0, 1, 00 -> 11 => 4 + 2 = 6
'''
```

---
Link: [[LeetCode]]
