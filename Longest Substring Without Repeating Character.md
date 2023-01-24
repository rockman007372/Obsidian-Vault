2022-06-05 16:44
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Longest Substring Without Repeating Character
### Questions
Input: a string
Output: the longest substring without a repeating character

### Solution
[[Sliding Window]] - in particular, [[Fast-Slow Sliding Window]] with a twist.

The lo pointer need not increment one by one and the character need not be removed one by one.

Instead, just move the lo pointer to the position index of the repeating character + 1. (If the position index + 1 < lo index, stay at low index).

```Java 
class Solution {
    public int lengthOfLongestSubstring(String s) {    
        HashMap<Character, Integer> map = new HashMap<>();
        int lo = 0;
        int longestRes = 0;
        
        for (int hi = 0; hi < s.length(); hi++) {
            if (map.containsKey(s.charAt(hi))) {
                lo = Math.max(lo, map.get(s.charAt(hi)));
            } 
            longestRes = Math.max(longestRes, hi - lo + 1);
            map.put(s.charAt(hi), hi + 1);
        }
        
        return longestRes;
    }
}
```

Time: O(n) < O(2n)
Space: O(min(m, n)), where n is length of string, m is the number of unique characters

More intuitive code:
```Java
public int lengthOfLongestSubstring(String s) {
        
        Map<Character, Integer> map = new HashMap<>();
        int lo = 0, len = 0;
        
        for (int hi = 0; hi < s.length(); i++) {
            char c = s.charAt(hi);
            if (map.containsKey(c)) {
                if (map.get(c) >= lo) 
                    lo = map.get(c) + 1;
            }
            len = Math.max(len, hi - lo + 1);
            map.put(c, hi);
        }
        
        return len;
    }
```