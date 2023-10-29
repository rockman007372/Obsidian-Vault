---
tags:
  - LeetCode
  - leetcode
topics: binaryTree, recursion
difficulty: 
performance: 
date: 2023-10-26 Thursday
---

## Questions

We build a table of `n` rows (**1-indexed**). We start by writing `0` in the `1st` row. Now in every subsequent row, we look at the previous row and replace each occurrence of `0` with `01`, and each occurrence of `1` with `10`.

- For example, for `n = 3`, the `1st` row is `0`, the `2nd` row is `01`, and the `3rd` row is `0110`.

Given two integer `n` and `k`, return the `kth` (**1-indexed**) symbol in the `nth` row of a table of `n` rows.

## Solution

Idea is the kth bit is either on the left or right side of the tree at any point, hence we just recurse/iterate on the correct half. Since there are a total O(2^N) nodes, run time is O(N).

### Recursion

### Iterative 

```python
class Solution:
    def kthGrammar(self, n: int, k: int) -> int:
        currLevel = 1
        bit = 0 
        index = k
        while currLevel < n:
            size = 2**(n - currLevel)
            half = size // 2
            if index > half:
                bit = bit ^ 1
                index = index - half
            currLevel += 1
            
        return bit

'''
0
01 
0110 
0110 1001
01101001 10010110
'''
```

Time: O(N)
Space: O(1)

---
Link: [[LeetCode]]
