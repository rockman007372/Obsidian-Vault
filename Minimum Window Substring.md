2022-06-05 16:44
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
## Question
Input: String S, String T
Output: Minimum length of the substring of S that contains all the characters in T.

## Solution

### Sliding Window

Idea: [[Fast-Slow Sliding Window]]

1.  We start with two pointers, `left` and `right` initially pointing to the first element of the string SS.
2.  We use the `right` pointer to expand the window until we get a desirable window i.e. a window that contains all of the characters of TT.
3.  Once we have a window with all the characters, we can move the `left` pointer ahead one by one. If the window is still a desirable one we keep on updating the minimum window size.
4.  If the window is not desirable any more, we repeat step 2 onwards

```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        
        if len(s) < len(t):
            return ''
        
        tCounter = Counter(t)
        required = len(tCounter) # THE UNIQUE NUMBER OF CHARACTERS IN T 
        
        lo, hi = 0, 0
        res = (None, lo, hi) # store (length, lo, hi)
        sCounter = defaultdict(int)
        current = 0
        while hi < len(s):
            sCounter[s[hi]] += 1 # increment window size
            
            if s[hi] in tCounter and sCounter[s[hi]] == tCounter[s[hi]]:
                current += 1
                
            # if we found a valid substring,
            # reduce window size to find min valid substring
            while lo <= hi and current == required: 
                # find min window size so far
                minLen = res[0]
                if not minLen or minLen > hi - lo + 1:
                    res = (hi - lo + 1, lo, hi)
                
                sCounter[s[lo]] -= 1 # increment lo
                
                if s[lo] in tCounter and sCounter[s[lo]] < tCounter[s[lo]]:
                    current -= 1
                
                lo += 1
                
            hi += 1
            
        return s[res[1] : res[2] + 1] if res[0] else ''
```

Time: O(S + T)
Worst case 2 pointers traverse O(2S) string. O(T) to traverse string T to initialize Hashmap ⇒ `O(2*S + T)`

Space: O(T)
O(T) = size of Hash Map to keep all unique characters in t

Takeaways:
- `Counter(t)` to quickly build dictionary 
- `defaultdict(int)` to generate default 0 
- Need to keep track of number of unique chars in anagram questions

### Optimized Sliding Window

Instead of going through every character in S, we can filter S to get only the characters in T.

```
S = "ABCDDDDDDEEAFFBC" T = "ABC"

filtered_S = [(0, 'A'), (1, 'B'), (2, 'C'), (11, 'A'), (14, 'B'), (15, 'C')]

Here (0, 'A') means in string S character A is at index 0.
```

Then, perform sliding window on filtered S. Time Complexity is reduced to:
`O(2 * |filtered_S| + |S| + |T|)` especially when `2|filtered_S| <<< |S|`

```Java
class Solution {
    public String minWindow(String s, String t) {

        if (s.length() == 0 || t.length() == 0) {
            return "";
        }

        Map<Character, Integer> dictT = new HashMap<Character, Integer>();

        for (int i = 0; i < t.length(); i++) {
            int count = dictT.getOrDefault(t.charAt(i), 0);
            dictT.put(t.charAt(i), count + 1);
        }

        int required = dictT.size();

        // Filter all the characters from s into a new list along with their index.
        // The filtering criteria is that the character should be present in t.
        List<Pair<Integer, Character>> filteredS = new ArrayList<Pair<Integer, Character>>();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (dictT.containsKey(c)) {
                filteredS.add(new Pair<Integer, Character>(i, c));
            }
        }

        int l = 0, r = 0, formed = 0;
        Map<Character, Integer> windowCounts = new HashMap<Character, Integer>();  
        int[] ans = {-1, 0, 0};

        // Look for the characters only in the filtered list instead of entire s.
        // This helps to reduce our search.
        // Hence, we follow the sliding window approach on as small list.
        while (r < filteredS.size()) {
            char c = filteredS.get(r).getValue();
            int count = windowCounts.getOrDefault(c, 0);
            windowCounts.put(c, count + 1);

            if (dictT.containsKey(c) && windowCounts.get(c).intValue() == dictT.get(c).intValue()) {
                formed++;
            }

            // Try and contract the window till the point where it ceases to be 'desirable'.
            while (l <= r && formed == required) {
                c = filteredS.get(l).getValue();

                // Save the smallest window until now.
                int end = filteredS.get(r).getKey();
                int start = filteredS.get(l).getKey();
                if (ans[0] == -1 || end - start + 1 < ans[0]) {
                    ans[0] = end - start + 1;
                    ans[1] = start;
                    ans[2] = end;
                }

                windowCounts.put(c, windowCounts.get(c) - 1);
                if (dictT.containsKey(c) && windowCounts.get(c).intValue() < dictT.get(c).intValue()) {
                    formed--;
                }
                l++;
            }
            r++;   
        }
        return ans[0] == -1 ? "" : s.substring(ans[1], ans[2] + 1);
    }
}
```