---
tags: LeetCode
topics: sliding window
difficulty: medium
performance: uncomplete
date: 2023-01-11 Wednesday
---

[[Sliding Window]], [[Group Anagram]]

## Questions

Given two strings `s` and `p`, return _an array of all the start indices of_ `p`_'s anagrams in_ `s`. You may return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

**Input:** `s = "cbaebabacd", p = "abc"`
**Output:** `[0,6]`
**Explanation:**
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".

**Example 2:**

**Input:** `s = "abab", p = "ab"`
**Output:** `[0,1,2]`
**Explanation:**
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".

## Solution

### Array

Idea:
- Keep an array counter for string p. Keep track of a window of size Np in string S.
- If the window in S is equal to P counter, we found an anagram
- Increment the window in S by shifting lo and hi pointer by 1.

```python
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        res = []
        ns, np = len(s), len(p)
        
        if len(s) < len(p):
            return res
            
        pCount, sCount = [0] * 26, [0] * 26
        
        # build frequency map of p
        for letter in p:
            pCount[ord(letter) - ord('a')] += 1
        
        for i in range(ns):
	        # increment hi pointer
            sCount[ord(s[i]) - ord('a')] += 1
			
			# Increment lo pointer
            if i >= np: # sliding window has fixed length of np
                index = ord(s[i - np]) - ord('a')
                sCount[index] -= 1
                
            if pCount == sCount: # O(26) = O(1) comparison
                res.append(i - np + 1)
            
        return res
```

Time: `O(Np + Ns) = O(Ns)`. Array size is fixed, hence O(1) comparison between 2 counters.
Space: `O(26) = O(1)`