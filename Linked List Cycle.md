2022-06-05 16:44
Tags: [[LeetCode]] - [[Linked List]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
##### Method 1: [[Hash Table]]
Space: O(N)

##### Method 2: Destructively modify linked list
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

##### Method 3 : two pointers aka [[Floyed's Cycle Finding Algorithm]]
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
	+ Traverse linked list using two pointers.
	+ Move one pointer(slow) by one and another pointer(fast) by two.
	+ If these pointers meet at the same node then there is a loop. If pointers do not meet then linked list doesn’t have a loop
+ If one pointer has double the speed, it will traverse 2 cycle (2N) after the the slower pointer traverses 1 cycle.

