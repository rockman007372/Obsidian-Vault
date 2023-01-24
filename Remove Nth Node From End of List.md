2022-06-05 16:44
Tags: [[LeetCode]] - [[Linked List]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Remove Nth Node From End of List
### Questions
Input: Head of a linked list, int N 
Output: A linked list with nth node from end removed

### Solution
Using 2 pointers, maintain n-node distance between the 2 pointers and move forward. Then do the modification after hi pointer reach the end.
Time: O(n)
Space: O(1)

```Java 
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode original = head;
        ListNode predecessor = new ListNode(-1);
        ListNode lo = head;
        ListNode hi = head;
        
        for (int i = 1; i < n; i++) {
            hi = hi.next;
        }
        
        while (hi.next != null) {
            predecessor = lo;
            lo = lo.next;
            hi = hi.next;
        }
        
        if (original == lo) {
            return lo.next;
        }
        
        predecessor.next = lo.next;
        lo.next = null; 
        return original;
    }
}
```

Instead of updating the predecessor node, create a dummy node, point both pointers to dummy node, then increment hi pointer so that there are n nodes IN BETWEEN them (n+1-node distance). Move to the end, modify and return `dummy.next` instead of `head`

```Java 
public ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode first = dummy;
    ListNode second = dummy;
    // Advances first pointer so that the gap between first and second is n nodes apart
    for (int i = 1; i <= n + 1; i++) {
        first = first.next;
    }
    // Move first to the end, maintaining the gap
    while (first != null) {
        first = first.next;
        second = second.next;
    }
    second.next = second.next.next;
    return dummy.next;
}
```