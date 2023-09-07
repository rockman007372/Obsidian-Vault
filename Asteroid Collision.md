---
tags: LeetCode, leetcode
topics: 
difficulty:
performance:
date: 2023-07-20 Thursday
---

## Questions

We are given an array `asteroids` of integers representing asteroids in a row.

For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.

**Example 1:**

```
Input: asteroids = [5,10,-5]
Output: [5,10]
Explanation: The 10 and -5 collide resulting in 10. The 5 and 10 never collide.
```

**Example 2:**

```
Input: asteroids = [8,-8]
Output: []
Explanation: The 8 and -8 collide exploding each other.
```

## Solution

>[!Reminder]
> All pair matching problem can probably be solved with a **stack**

Key idea:
- Maintain a stack to process the asteroids we have seen
- Compare the current asteroid with the ones in the stack

Time: O(N)
- Each asteroid can be added and removed at most 2 times from the stack!

Space: O(N)

```python
class Solution:
    def asteroidCollision(self, asteroids: List[int]) -> List[int]:
    
        stack = [asteroids[0]]

        for asteroid in asteroids[1:]:
            explode = False

            while stack:
                if (stack[-1] * asteroid > 0) or (stack[-1] < 0 and asteroid > 0):
                    break
                else:
                    if abs(stack[-1]) == abs(asteroid):
                        explode = True
                        stack.pop()
                        break

                    if abs(stack[-1]) > abs(asteroid):
                        explode = True
                        break

                    if abs(stack[-1]) < abs(asteroid):
                        stack.pop()
            
            if not explode:
                stack.append(asteroid)
        
        return stack
```

---
Link: [[LeetCode]]
