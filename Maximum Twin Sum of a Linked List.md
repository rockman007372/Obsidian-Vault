---
tags: LeetCode, leetcode
topics: twoPointers
difficulty: medium
performance: uncomplete
date: 2023-05-18 Thursday
---

## Questions

In a linked list of size `n`, where `n` is **even**, the `ith` node (**0-indexed**) of the linked list is known as the **twin** of the `(n-1-i)th` node, if `0 <= i <= (n / 2) - 1`.

-   For example, if `n = 4`, then node `0` is the twin of node `3`, and node `1` is the twin of node `2`. These are the only nodes with twins for `n = 4`.

The **twin sum** is defined as the sum of a node and its twin.

Given the `head` of a linked list with even length, return _the **maximum twin sum** of the linked list_.


## Solution

### In-place listed list reversal

Idea:
- Reverse the right half of the linked list and compare each pair
- How to find middle node? **Slow-fast pointers**

Time: O(N)
Space: O(1)

```python
class Solution:

    def reverse(self, head):
        prev = None
        while head:
            temp = head.next
            head.next = prev
            prev = head
            head = temp
        return prev

    def pairSum(self, head: Optional[ListNode]) -> int:
        # obtain middle node
        slow = head
        fast = head

        while fast:
            slow = slow.next
            fast = fast.next.next

        # reverse right-half of list
        reversedHead = self.reverse(slow)

        # iterate through each pair and find max
        result = -1
        while head != slow:
            result = max(result, head.val + reversedHead.val)
            head = head.next
            reversedHead = reversedHead.next
        
        return result
```

---
Link: [[LeetCode]]
