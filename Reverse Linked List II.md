2022-07-08 11:05
Tags: [[LeetCode]] - [[Reverse Linked List]] - [[Linked List]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Reverse Linked List II
### My Performance
#complete #notOnTime 

### Questions
Difficulty: #medium 
Input: a Linked List and left, right integers.
Output: a modified linked list s.t the linked list in between the integers is reversed.

### Solution
##### Recursion
Involves swapping the value of the node, not the node itself -> destructive modification = bad.
However, it has the interesting idea of using backtracking of recursion to traverse the linked list backwards!

##### One pass interative
Time: O(N)
Space: O(1)

```Java
class Solution {
    public ListNode reverseBetween(ListNode head, int left, int right) {
        ListNode root = new ListNode();
        root.next = head;
        ListNode prehead = root;
        // traverse to reverse part
        for (int i = 1; i < left; i++) {
            prehead = prehead.next;
        }
        
        // reverse 
        ListNode subhead = prehead.next;
        ListNode rev = null;
        for (int j = left; j <= right; j++) {
            ListNode temp = subhead.next;
            subhead.next = rev;
            rev = subhead;
            subhead = temp;
        }
        
        // 2 ends modification
        prehead.next.next = subhead; // connect the end
        prehead.next = rev; // connect the start
        
        return root.next;
    }
}
```