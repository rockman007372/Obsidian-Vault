---
tags: LeetCode
topics: [DynamicProgramming, Memoization]
difficulty: medium
performance: uncomplete
---
Date:: 2022-08-02 Tuesday
Tags: [[LeetCode]] - [[Memoization]] - [[Dynamic Programming]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Word Break
### My Performance
#uncomplete 

### Questions
Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

**Note** that the same word in the dictionary may be reused multiple times in the segmentation.

**Example 1:**

>**Input:** s = "leetcode", wordDict = ["leet","code"]
**Output:** true
**Explanation:** Return true because "leetcode" can be segmented as "leet code".

**Example 2:**

>**Input:** s = "applepenapple", wordDict = ["apple","pen"]
**Output:** true
**Explanation:** Return true because "applepenapple" can be segmented as "apple pen apple".
Note that you are allowed to reuse a dictionary word.

**Example 3:**

>**Input:** s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
**Output:** false

Difficulty: #medium 
Input: `String` s and `List` wordDict
Output: `boolean` can String s be seperated into sequences of words

### Solution

#####  Brute Force
- Use [[Recursion]] and [[Backtracking]]
- Starting from begining, we split the string if the first substring matches the word in the dictionary, and recurse on the remaining substring. 
- If the remaining substring does not form a word sequence, we backtrack.
- At each character, we either split the word there or we dont. Since there are N characters, we can have O(2^N) ways to split -> Time complexity = O(2^N)

##### Top-Down Memoization
Idea: 
- For each word in dictionary, check if the substring starting from the begining of string s is equal to the word.
- If true, we reduce the string s to a smaller substring, and repeat the process.
- Memoization is used to cache substring between i and the end that cannot be broken down into words.

![[Pasted image 20220803012435.png]]

Time: O(N * M * N) loosely -> O(?) with memoization?
- Tree of max height N
- M children on each level
- O(N) length to compare 2 strings
- Eg: `input="aaaab"`, `dictionary = {"a", "aa", "aaa", "aaaa"}`

Space: O(N) - cache of size N and recursion stack is O(N) deep (when word is one character long)

```Java
class Solution {
    private HashSet<Integer> cache;
    public boolean wordBreak(String s, List<String> wordDict) {
        cache = new HashSet<>();
        return helper(s, wordDict, 0);
    }
    
    private boolean helper(String s, List<String> wordDict, int idx) {
        if (idx == s.length()) {
            return true;
        }
        
        if (cache.contains(idx)) return false;
        
        boolean ans = false;
        for (String word : wordDict) {
            int wordLen = idx + word.length();
            if (wordLen > s.length()) continue;
            
            String substring = s.substring(idx, wordLen);
            if (substring.equals(word)) {
                ans = helper(s, wordDict, wordLen);
            }
            
            if (ans == true) return true;
        }
        
        cache.add(idx);
        return false;
    }
}
```

##### Bottom-up DP
- State: `DP[i]` = true if there is a valid word sequence from i to end
- Relation: `DP[i] = DP[i + j]` where j is the length of the word in wordDict, if the substring btw i and j forms a valid word.
- Time: O($N * M * N$)
- Space: O(N)
  
```Java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        int len = s.length();
        boolean[] DP = new boolean[len + 1];
        DP[len] = true;
        
        for (int i = len - 1; i >= 0; i--) {
            for (String word : wordDict) {
                int wordLen = i + word.length();
                if (wordLen <= len) {
                    if (s.substring(i, wordLen).equals(word)) {
                        DP[i] = DP[wordLen];
                        
                        if (DP[i] == true) break;
                    }
                }
            }
        }
        
        return DP[0];
    }
}
```