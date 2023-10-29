---
tags:
  - LeetCode
  - leetcode
topics: linkedList, cycle
difficulty: medium
performance: uncomplete
date: 2022-07-24 Sunday
---
tag: [[Linked List]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
## Hash table

Use a hash table to keep track of duplicated nodes.
Space: O(N)

## Method 2: Destructively modify linked list

```Java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) return false;
        if (head.next == head) return true;
        ListNode temp = head.next;
        head.next = head;
        return hasCycle(temp);
    }
}
```

## Method 3 : two pointers aka [[Floyed's Cycle Finding Algorithm]]

```Java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null) {
            return false;
        }

        ListNode slow = head;
        ListNode fast = head.next;
        while (slow != fast) {
            if (fast == null || fast.next == null) {
                return false;
            }
            slow = slow.next;
            fast = fast.next.next;
        }
        return true;
    }
}
```

+ Idea: 
	+ Traverse linked list using two pointers, slow and fast.
	+ Move `slow` by one and `fast` by two. (double the speed)
	+ If these pointers meet at the same node then there is a loop. If pointers do not meet then linked list doesn’t have a loop
+ If 2 pointers start at the same point in the cycle, the faster pointer will have traversed 2 cycles (2N) after the the slower pointer traverses 1 cycle.
+ If they start at different points in the cycle, the fast pointer would still catch up with the slow pointer at some point (instead of cycle, imagine an infinitely long line.)

