2022-06-05 16:44
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Longest Palindrome

## Questions
Given a string `s` which consists of lowercase or uppercase letters, return _the length of the **longest palindrome**_ that can be built with those letters.

Letters are **case sensitive**, for example, `"Aa"` is not considered a palindrome here.

>**Input:** s = "abccccdd"
**Output:** 7
**Explanation:** One longest palindrome that can be built is "dccaccd", whose length is 7.

## Solution
#### Greedy with HashMap
- Make use of [[Hash Table]]
- Palindrome characters either appear all in *even* frenquency or with one *odd* central character ("bb aa bb" or "bba a abb").

```Java
// My solution
class Solution {
    public int longestPalindrome(String s) {
	    // update frequency of characters
        HashMap<Character, Integer> freq = new HashMap<>();
        for (int i = 0, len = s.length(); i < len; i++) {
            char c = s.charAt(i);
            freq.put(c, freq.getOrDefault(c, 0) + 1);
        }
        
        int res = 0;
        boolean odd = false;
        for (int frequency : freq.values()) {  
            if (frequency % 2 == 0) {
                res += frequency;
                continue;
            }
            
            // if frequency is odd
            res += frequency - 1;
            
            if (!odd) {
                odd = true;
            }
        }
        return odd ? res + 1 : res;
    }
}
```

```Java
// Super clean one pass
// where we get char frequency and 
// update max length of palindrome simultaneously
class Solution {
    public int longestPalindrome(String s) {
        int[] count = new int[128];
        int length = 0;
        for (char c: s.toCharArray()){
            if (++count[c] == 2){
                length += 2;
                count[c] = 0;
            }
        }
        return (length == s.length()) ? length : length + 1;
    }
}
```