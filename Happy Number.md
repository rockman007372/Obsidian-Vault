---
tags: LeetCode
topics: implementation
difficulty: easy
performance: complete
date: 2022-12-08 Thursday
---

### Questions
Write an algorithm to determine if a number `n` is happy.

A **happy number** is a number defined by the following process:

-   Starting with any positive integer, replace the number by the sum of the squares of its digits.
-   Repeat the process until the number equals 1 (where it will stay), or it **loops endlessly in a cycle** which does not include 1.
-   Those numbers for which this process **ends in 1** are happy.

Return `true`  if  `n`  is a happy number, and  `false`  if not.

### Solution 1

There are 3 cases
1. Sum goes to 1
2. Sum loops in a cycle
3. Sum goes to infinity

However, case 3 can never happen! 

| Digits | Largest  | Next |
| ------ | -------- | ---- |
| 1      | 9        | 81   |
| 2      | 99       | 162  |
| 3      | 999      | 243  |
| 4      | 9999     | 324  |
| 13     | 99999... | 1053 | 

- For numbers with 3 digits, the largest sum it can reach is 243. Once a number is below 243, it is impossible for it to go back up above 243. 
- For number with 4 digits, **it will always lose 1 digit and revert back to 3 digits**. 
- For all the numbers in the given range, the sum has 4 digits maximally, hence the sum will always loop back to never exceeding 243. 


```python
class Solution:

    def isHappy(self, n: int) -> bool:

        # Sum of squared digits
        def square_sum(num : int):
            SSum = 0
            while num != 0:
                SSum += ((num % 10) ** 2)
                num = int(num / 10)
            return SSum

        res = n
        cache = set()

        # check for cycles
        while res != 1:
            res = square_sum(res)
            if res in cache:
                return False
            cache.add(res)
            
        return True    
        
"""
# Algorithm:

1. sum the squares of the digit
2. repeat on the computed sum
3. if sum is eventually 1, returns true

constraints:

1. if sum = 1, 10, 100, 1000, 10000... then it is a happy number
2. sum is sum of 2 squared number - is 1000 a sum of 2 squared number?

How to know when to stop the loop? (loop infinitely): If it loops in a cycle (check duplicates)
"""
```

Time: $O(lg(n))$ 
- Finding the next sum takes $O(lg(n))$ as there are $lg(n)$ digits in n
- We break the analysis into 2 steps:
	- The amount of time it takes to reach 243: $$log(n) + log(log(n)) + ...=O(log(n))$$
	- Once the sum reaches 243 threshold, the amount of time it takes to either discover a cycle or converge to 1 is $O(243 * 3)$ where 243 is the max number of steps and 3 is the number of digits (since by now all sum will have maximally 3 digits). This is reduced to $O(1)$

Space: $O(lg(n))$



### Solution 2: [[Floyed's Cycle Finding Algorithm]]

```python
def isHappy(self, n: int) -> bool:  
    def get_next(number):
        total_sum = 0
        while number > 0:
            number, digit = divmod(number, 10)
            total_sum += digit ** 2
        return total_sum

    slow_runner = n
    fast_runner = get_next(n)
    while fast_runner != 1 and slow_runner != fast_runner:
        slow_runner = get_next(slow_runner)
        fast_runner = get_next(get_next(fast_runner))
    return fast_runner == 1
```

Time: O(lg(N))
Space: O(1) - no need Hash Set to detect cycle.