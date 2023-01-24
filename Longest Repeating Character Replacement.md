2022-06-05 16:44
Tags: [[LeetCode]] - [[Sliding Window]] - [[Hash Table]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
## Question
You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.

Return _the length of the longest substring containing the same letter you can get after performing the above operations_.

**Input:** s = "AABABBA", k = 1
**Output:** 4
**Explanation:** Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.

## Solution 
So difficult :(

+ Maintain 2 pointers lo and hi, which restrict a window
+ Constant result indicates the longest **REPEATING** string within the window
+ maxFrequency stores the character with the most frequency so far (so we can replace the remaining unmatched character)
+ [[Fast-Slow Sliding Window]] method, with constraint that `length (hi - lo + 1) - maxFrequency` >  `k`.
   
```Java
class Solution {
    public int characterReplacement(String s, int k) {
        if (s.length() == 1) {
            return 0;
        }
    
        int[] charCount = new int[26];
        Arrays.fill(charCount, 0);
        int maxFrequency = 0;
        int res = 0;
        int lo = 0;
        for (int hi = 0; hi < s.length(); hi++) {
            int index = s.charAt(hi) - 'A';
            charCount[index]++;
            
            // update maxFrequency (only care about maxFrequency so far)
		    maxFrequency = Math.max(maxFrequency, charCount[index])
            
            // if we exceed max number of characters replacable
            while (hi - lo + 1 - maxFrequency > k) {
                charCount[s.charAt(lo) - 'A']--;
                lo++; //increase lo pointer to shrink the window and find a REPEATING string
            }
            res = Math.max(res, hi - lo + 1); // at this point, hi - lo + 1 indicates the longest repeating string in that window
        }
        return res;
    }
}

```

+ Time: O(2N) = O(N)
+ Space: O(1)

