---
tags:
  - LeetCode
  - leetcode
topics: linkedList, cycle
difficulty: medium
performance: 
date: 2022-07-24 Sunday
---
 
## Questions

Input: linked list
Output: the middle node of the linked list

## Solution
### Fast and Slow Pointer

- Similar to [[Floyed's Cycle Finding Algorithm]].
- Maintain 2 pointers, one is twice as fast as the other. If the fast pointer reaches the end of the list, the slow pointer must be at the middle!

```Java
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
}
```