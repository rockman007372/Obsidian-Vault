---
tags: LeetCode
topics: sort
difficulty: easy
performance: complete
date: 2023-01-06 Friday
---

### Questions

You are given an array of `n` strings `strs`, all of the same length.

The strings can be arranged such that there is one on each line, making a grid. For example, `strs = ["abc", "bce", "cae"]` can be arranged as:

abc
bce
cae

You want to **delete** the columns that are **not sorted lexicographically**. In the above example (0-indexed), columns 0 (`'a'`, `'b'`, `'c'`) and 2 (`'c'`, `'e'`, `'e'`) are sorted while column 1 (`'b'`, `'c'`, `'a'`) is not, so you would delete column 1.

Return _the number of columns that you will delete_.

### Solution

##### Sort and Compare Each Column

```python
class Solution:
    def minDeletionSize(self, strs: List[str]) -> int:
        l = len(strs[0])

        count = 0
        for i in range(l):
            sorted_strs = sorted(strs, key = lambda x : x[i])
            if sorted_strs != strs:
                count += 1

        return count
```

Time: O(L * NlogN)
Space: O(N) or O(lgN)

##### Compare Letter by Letter

```python
class Solution:
    def minDeletionSize(self, strs: List[str]) -> int:
        l = len(strs[0])
        count = 0
        for i in range(l):
            for n in range(1, len(strs)):
                if strs[n][i] < strs[n - 1][i]:
                    count += 1
                    break
        return count
```

Time: O(L * N)
Space: O(1)