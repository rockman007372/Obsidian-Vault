---
tags: LeetCode
topics: two pointers
difficulty: medium
performance: uncomplete
date: 2023-01-09 Monday
---

### Questions

Input:
Output: 

### Solution

Biggest takeaway is to handle edge cases involving the head by creating a sentinel!

```
[1, 1, 2] ⇒ [2]

sentinel → 1 → 1 → 2

```

##### My shitty solution

```python
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:

        if not head or not head.next:
            return head

        sentinel = ListNode(None, head)

        lo, hi = sentinel, sentinel.next

        while True:
            
            # increment lo and hi if hi.next is not a duplicate
            while hi.next and hi.val != hi.next.val:
                lo = lo.next
                hi = hi.next
            # edge case 
            if not hi.next:
                break
                
            # manipulate list if hi.next is a duplicate
            while hi.next and hi.val == hi.next.val:
                hi = hi.next        
            lo.next = hi.next
            if not hi.next:
                break
            hi = hi.next
            
        return sentinel.next
```

Time: O(N)
Space: O(1)


### Short Iterative Solution

```python
class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        # sentinel
        sentinel = ListNode(0, head)

        # predecessor = the last node 
        # before the sublist of duplicates
        pred = sentinel
        
        while head:
            # if it's a beginning of duplicates sublist 
            # skip all duplicates
            if head.next and head.val == head.next.val:
                # move till the end of duplicates sublist
                while head.next and head.val == head.next.val:
                    head = head.next
                # skip all duplicates
                pred.next = head.next 
            # otherwise, move predecessor
            else:
                pred = pred.next 
                
            # move forward
            head = head.next
            
        return sentinel.next
```

##### Cool Recursive Solution

```python
class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head
        if head.val == head.next.val:
            # skip duplicate nodes
            while head.next and head.val == head.next.val:
                head = head.next
            return self.deleteDuplicates(head.next)
        else:
            head.next = self.deleteDuplicates(head.next)
            return head
```

But space is O(N)