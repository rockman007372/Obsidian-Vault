---
tags: LeetCode
topics: counting
difficulty: medium
performance: uncomplete
date: 2023-01-05 Thursday
---

### Questions

You are given a **0-indexed** integer array `tasks`, where `tasks[i]` represents the difficulty level of a task. In each round, you can complete either 2 or 3 tasks of the **same difficulty level**.

Return _the **minimum** rounds required to complete all the tasks, or_ `-1` _if it is not possible to complete all the tasks._

### Solution

![[Pasted image 20230105225103.png]]

```python
class Solution:
    def minimumRounds(self, tasks: List[int]) -> int:
        frequency = {}

        for task in tasks:
            if task in frequency:
                frequency[task] += 1
            else:
                frequency[task] = 1

        count = 0
        for num in frequency.values():
            if num < 2:
                return -1
            elif num % 3 == 0:
                count += num // 3
            else:
                count += num // 3 + 1
        return count
```

Time: O(N)
Space: O(N)