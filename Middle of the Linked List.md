2022-06-05 16:44
Tags: [[LeetCode]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Middle of the Linked List
## My Performance

## Questions
Input:
Output: 

## Solution
#### Similar to [[Floyed's Cycle Finding Algorithm]] - [[Linked List Cycle]]
Maintain 2 pointers, one is twice as fast as the other!

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