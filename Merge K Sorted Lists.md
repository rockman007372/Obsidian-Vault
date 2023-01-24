2022-06-05 16:44
Tags: [[LeetCode]] - [[Merge Two Sorted Lists]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Merge K Sorted Lists
## My Performance
#uncomplete 

## Questions
Input: Lists of sorted linked lists
Output: One single merged sorted linked list

## Solution
#### Divide and Conquer Algorithm - Most Optimal Time and Space

![[Pasted image 20220702230201.png]]

Idea: Similar to [[Merge Sort]].

Time: O(N * LogK), where N is the TOTAL number of nodes in the list of linked lists, and K is the number of linked lists in the list.

![[Merge K Sorted Lists 2022-07-02 23.03.29.excalidraw|700]]

Space: O(lgK) : Recursion stack depth

```Java
 // My solution
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        int len = lists.length - 1;
        if (len == -1) return null;
        return mergeKHelper(lists, 0, len); // 0, 2
    }
    
    public ListNode mergeKHelper(ListNode[] lists, int lo, int hi) {
        if (lo == hi) return lists[lo];
        int mid = lo + (hi - lo) / 2;
        return merge(
            mergeKHelper(lists, lo, mid), // 0, 1
            mergeKHelper(lists, mid + 1, hi) // 2, 2
        );
    }
    
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
}
```

Iterative Merge Sort (Bottom-up) - Space: O(1)

```Java
// Optimal space solution
public ListNode mergeKLists(ListNode[] lists) {
    if(lists.length==0){
        return null;
    }
    int interval = 1;
    while(interval<lists.length){
        for (int i = 0; i + interval< lists.length; i=i+interval*2) {
            lists[i]=mergeTwoLists(lists[i],lists[i+interval]);            
        }
        interval*=2;
    }
    return lists[0];
}
```

#### Priority Queue - [[Heap]]
Idea: Maintain a MinHeap of first k List Nodes. As we extractMin, we add the next List Node into the Min Heap to maintain k size. 

Time: O(N * lgK)
- Add and remove a node take O(lgK)
- There are a total of N nodes in the final linked list

Space: O(k) - Size of MinHeap

```Java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        int len = lists.length;
        if (len == 0) return null;
        
        // create a comparator for ListNodes to sort Min Heap
        Comparator<ListNode> nodeComparator = new Comparator<>() {
            @Override
            public int compare(ListNode x, ListNode y) {
                return x.val - y.val;
            }
        };
        
        // create a Min Heap using the comparitor
        PriorityQueue<ListNode> minHeap = 
	        new PriorityQueue<>(len, nodeComparator);
        
        // add initial k nodes to min Heap
        for (ListNode node : lists) {
            if (node != null) {
                minHeap.add(node);                
            }
        }
        
        // extract min and add the next node
        ListNode root = new ListNode();
        ListNode preHead = root;
        while (!minHeap.isEmpty()) {
            ListNode curr = minHeap.poll();
            root.next = curr;
            root = root.next;
            if (curr.next != null) {
                minHeap.add(curr.next);
            }
        }
        return preHead.next;
    }
}
```