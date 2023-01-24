---
tags: LeetCode
topics: stack, pointers
difficulty: medium
performance: complete, notOptimal
date: 2023-01-10 Tuesday
---

### Questions

Given two strings `s` and `t`, return `true` _if they are equal when both are typed into empty text editors_. `'#'` means a backspace character.

Note that after backspacing an empty text, the text will continue empty.

**Example 1:**

**Input:** s = "ab#c", t = "ad#c"
**Output:** true
**Explanation:** Both s and t become "ac".

**Example 2:**

**Input:** s = "ab##", t = "c#d#"
**Output:** true
**Explanation:** Both s and t become "".

### Solution

##### Stack O(N) Space

```python
class Solution:
    def backspaceCompare(self, s: str, t: str) -> bool:
        stack1 = []
        stack2 = []

        for char1 in s:
            if char1 == '#':
                if stack1:
                    stack1.pop()
            else: 
                stack1.append(char1)
        
        for char2 in t:
            if char2 == '#':
                if stack2:
                    stack2.pop()
            else:
                stack2.append(char2)

        return stack1 == stack2
```

##### Constant Space Solution using Pointer

Trick is to compare the string backwards and modify the pointers correctly. The invariant is if 2 strings are the same, then **at the end of any iteration the pointers must point to the same character.**

Time: O(N)
Space: O(1)

```python
class Solution:
    def backspaceCompare(self, s: str, t: str) -> bool:
        
        p1, p2 = len(s) - 1, len(t) - 1

        skip1, skip2 = 0, 0

        while p1 >= 0 or p2 >= 0: # not AND, else false negative
            
            # Find the next valid char in s
            while p1 >= 0:
                if s[p1] == '#':
                    skip1 += 1
                    p1 -= 1
                elif skip1:
                    skip1 -= 1
                    p1 -= 1
                else:
                    break

            # Find the next valid char in t
            while p2 >= 0:
                if t[p2] == '#':
                    skip2 += 1
                    p2 -= 1
                elif skip2:
                    skip2 -= 1
                    p2 -= 1
                else:
                    break
        
            # If the 2 corresponing char are not equal, false
            if p1 >= 0 and p2 >= 0 and s[p1] != t[p2]:
                return False
            elif p1 < 0 and p2 < 0:
                return True
            elif p1 < 0 or p2 < 0:
                return False

            p1 -= 1
            p2 -= 1

        return True # if reached here   
```


