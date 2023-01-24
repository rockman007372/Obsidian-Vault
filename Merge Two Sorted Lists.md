2022-06-05 16:44
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Merge Two Sorted Lists
## My Performance
#uncomplete ???

## Questions
Input: 2 sorted linked lists
Output: merged sorted list

## Solution
#### Recursion
```Java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        else if (l2 == null) {
            return l1;
        }
        else if (l1.val < l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        }
        else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }
    }
}
```

Time: O(M + N)
Space: O(Min(M, N))

#### Iterative
```Java
public ListNode merge(ListNode x, ListNode y) {
        if (x == null) return y;
        if (y == null) return x;
        
        ListNode root = new ListNode();
        ListNode prehead = root;
        
        while (x != null && y != null) {
            if (x.val <= y.val) {
                root.next = x;
                x = x.next;
            } else if (x.val > y.val) {
                root.next = y;
                y = y.next;
            }
            root = root.next;
        }
        
        // gather all the remaining elements at the end
        root.next = (x == null) ? y : x;
        return prehead.next;
        
    }
```

Time: O(M + N)
Space: O(1)