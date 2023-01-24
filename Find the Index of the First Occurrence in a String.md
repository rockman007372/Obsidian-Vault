---
tags: LeetCode, leetcode
topics: two pointers
difficulty: medium
performance: complete, notOptimal
date: 2023-01-15 Sunday
---

## Questions

Given two strings `needle` and `haystack`, return the index of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.

**Example 1:**

**Input:** haystack = "sadbutsad", needle = "sad"
**Output:** 0
**Explanation:** "sad" occurs at index 0 and 6.
The first occurrence is at index 0, so we return 0.

**Example 2:**

**Input:** haystack = "leetcode", needle = "leeto"
**Output:** -1
**Explanation:** "leeto" did not occur in "leetcode", so we return -1.

## Solution

### Brute Force: O(ST)

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if len(needle) > len(haystack):
            return -1
        for i in range(len(haystack) - len(needle) + 1): # O(S)
            if haystack[i: i + len(needle)] == needle: # O(T)
                return i
        return -1
```

Starting at each index, check if the substring starting from that index equals the needle.

Time: `O(T * (S - T + 1)) = O(ST)`
Space: O(1)

### KMP Algorithm O(S + T)

Very intuitive video [explanation](https://www.youtube.com/watch?v=EL4ZbRF587g) and text [explanation](http://jakeboxer.com/blog/2009/12/13/the-knuth-morris-pratt-algorithm-in-my-own-words/)

In the brute force solution, we have to increment `lo` pointer one by one to not miss any valid substring. In the KMP algorithm, we make use of the fact that inside the window we just checked there may be repeated characters that can form the correct pattern, and hence we have to adjust 'lo' pointer smartly only when needed. 

Big idea is to keep a Partial Match Table. We can use the values in the partial match table to skip ahead (rather than redoing unnecessary old comparisons) when we find partial matches. 

Here’s the partial match table for the pattern “abababca”:

```
char:  | a | b | a | b | a | b | c | a |
index: | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 
value: | 0 | 0 | 1 | 2 | 3 | 4 | 0 | 1 |
```

At index i, `table[i]` value gives the longest length of the prefix that is also a suffix in the window `[0, i]`.

For example, at index 5, the longest prefix and also suffix is 'abab', which has length of 4. At index 3, the longest prefix that is also a suffix is 'ab', which has length of 2.

KMP Algorithm:
- While the upper character of the window matches the upper character of the pattern, increment `hi` pointer to increase window size
- Once the upper character does not match, we increment lo pointer by `partial_match_length - table[partial_match_length - 1]`

Example:

```
text = `bacbababaabcbab`
pattern = 'abababca'
table = [0, 0, 1, 2, 3, 4, 0, 1]
```

The first time we get a partial match is here:

```
bacbababaabcbab
 |
 abababca
```

This is a partial_match_length of 1. The value at `table[partial_match_length - 1]` (or `table[0]`) is 0, so we don’t get to skip ahead any. The next partial match we get is here:

```
bacbababaabcbab
    |||||
    abababca
```

This is a partial_match_length of 5. The value at `table[partial_match_length - 1]` (or `table[4]`) is 3. That means we get to skip ahead `partial_match_length - table[partial_match_length - 1]` (or `5 - table[4]` or `5 - 3` or `2`) characters:

```
// x denotes a skip

bacbababaabcbab
    xx|||
      abababca
```

This is a partial_match_length of 3. The value at `table[partial_match_length - 1]` (or `table[2]`) is 1. That means we get to skip ahead `partial_match_length - table[partial_match_length - 1]` (or `3 - table[2]` or `3 - 1` or `2`) characters:

```
// x denotes a skip

bacbababaabcbab
      xx|
        abababca
```

At this point, our pattern is longer than the remaining characters in the text, so we know there’s no match.

---
Link: [[LeetCode]]