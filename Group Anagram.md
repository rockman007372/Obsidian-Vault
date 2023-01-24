---
tags: LeetCode
topics: hash, sort
difficulty: medium
performance: uncomplete
date: 2022-07-24 Sunday
---

## Questions
Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Solution
- Make use of [[Hash Table]]
- Anagrams have same numbers of letter ⇒ Create a **hashable count** and map to list of anagrams
![[Pasted image 20220605184724.png]]
- Time: O(NK), where N is the number of strings and K is the length of the longest string (in order the build the count)
- Space: O(NK), the size of ans?

``` Java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> res = new ArrayList<>();
        HashMap<String, List<String>> map = new HashMap<>();
        
        for (String s : strs) {
            int[] count = new int[26];
            Arrays.fill(count, 0);
            for (int i = 0; i < s.length(); i++) {
                count[s.charAt(i) - 'a']++; 
            }
            StringBuilder sb = new StringBuilder("");
            for (int i = 0; i < count.length; i++) {
                sb.append(count[i]);
                sb.append('#');
            }
            
            String hashable = sb.toString();
            if (!map.containsKey(hashable)) {
                map.put(hashable, new ArrayList<String>());
            }              
            map.get(hashable).add(s);
        }
        return new ArrayList<>(map.values());
    }
}
```

+ To create ArrayList from Collection: `new ArrayList<>(Collection)`

```Python
class Solution:
    def groupAnagrams(strs):
        ans = collections.defaultdict(list)
        for s in strs:
            count = [0] * 26
            for c in s:
                count[ord(c) - ord('a')] += 1
            ans[tuple(count)].append(s)
        return ans.values()

```

Learning points:
- `collections.default(list)` will create empty list as an element if there is no element in the list
- `ord('a')` returns the ascii value of char 'a'
- A tuple is hashable, while lists cannot because tuple is immutable.