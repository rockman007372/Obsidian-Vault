---
tags: LeetCode, leetcode
topics: linkedlist
difficulty: medium
performance: complete
date: 2023-05-16 Tuesday
---

## Questions

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg)

**Input:** `head = [1,2,3,4]`
**Output:** `[2,1,4,3]`

## Solution

### Recursive

Time and space: O(N)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if (not head) or (not head.next): return head 
        node=head.next 
        head.next=self.swapPairs(head.next.next) 
        node.next=head 
        return node 
```

---
Link: [[LeetCode]]
