---
tags: LeetCode, leetcode
topics: heap
difficulty: easy
performance: complete, notOnTime
date: 2023-05-23 Tuesday
---

## Questions

Design a class to find the `kth` largest element in a stream. Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

Implement `KthLargest` class:

-   `KthLargest(int k, int[] nums)` Initializes the object with the integer `k` and the stream of integers `nums`.
-   `int add(int val)` Appends the integer `val` to the stream and returns the element representing the `kth` largest element in the stream.

## Solution

```Java
class KthLargest {

    private int k;
    private Queue<Integer> minHeap = new PriorityQueue<>();
    
    public KthLargest(int k, int[] nums) {
        this.k = k;    
        for (int num : nums) {
            add(num); // use own add function! O(nlogk)
        }
    }
    
    public int add(int val) {
        minHeap.add(val);
        if (minHeap.size() > k) minHeap.poll();
        return minHeap.peek();
    }
}
```

---
Link: [[LeetCode]]
