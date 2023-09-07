---
tags: LeetCode, leetcode
topics: 
difficulty: easy
performance: complete, notOptimal
date: 2023-05-23 Tuesday
---

## Questions

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**

**Input:** strs = `["flower","flow","flight"]`
**Output:** `"fl"`

**Example 2:**

**Input:** strs = `["dog","racecar","car"]`
**Output:** `""`
**Explanation:** There is no common prefix among the input strings.

## Solution

Time: O(mn) = O(S)
- m is the average length of each string and n is the number of strings.
- S is the total characters in `strs`

Space: O(1)

```javascript
/**
 * @param {string[]} strs
 * @return {string}
 */
var longestCommonPrefix = function(strs) {

    var prefixHelper = (x, y) => {
        let len = Math.min(x.length, y.length);
        let i = 0;
        while (i < len) {
            if (x[i] != y[i]) {
                break;
            }
            i++;
        }
        return x.substring(0, i)
    };

    return strs.reduce((x, y) => prefixHelper(x, y), strs[0]);
};
```

---
Link: [[LeetCode]]
