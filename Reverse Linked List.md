2022-06-05 16:44
Tags: [[LeetCode]] - [[Linked List]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Reverse Linked List
### Main Points
##### Method 1: [[Recursion]]
Time: O(n)
Space: O(n) (max recursion stack space)
```Java
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        } else {
            ListNode temp = head.next;
            head.next = null;
            ListNode reversed = reverseList(temp);
            temp.next = head;
            return reversed; 
        }
    }
}
```

##### Method 2: [[Iterative]]
Time: O(N)
Space: O(1) no deferred operations

```Java 
class Solution {
    public ListNode reverseList(ListNode head) {
        return reverseHelper(head, null);   
    }
    
    public ListNode reverseHelper(ListNode head, ListNode reverse) {
        if (head == null) {
            return reverse;
        } else {
            ListNode temp = head.next;
            head.next = reverse;
            return reverseHelper(temp, head);
        }
    }
}
```

Using While loop:
```Java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode curr = head;
        while (curr != null) {
            ListNode nextTemp = curr.next;
            curr.next = prev;
            prev = curr; // update the reversed node
            curr = nextTemp; // traverse to the next node
        }
        return prev;
    }
}
```