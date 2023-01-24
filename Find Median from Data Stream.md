2022-07-05 15:54
Tags: [[LeetCode]] - [[Quick Select]] - [[Binary Search]] - [[Heap]] - [[AVL Tree]] - [[Binary Search Tree]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Find Median from Data Stream
### My Performance
#uncomplete 

### Questions
Difficulty: #hard

The **median** is the middle value in an ordered integer list. If the size of the list is even, there is no middle value and the median is the mean of the two middle values.

-   For example, for `arr = [2,3,4]`, the median is `3`.
-   For example, for `arr = [2,3]`, the median is `(2 + 3) / 2 = 2.5`.

Implement the MedianFinder class:

-   `MedianFinder()` initializes the `MedianFinder` object.
-   `void addNum(int num)` adds the integer `num` from the data stream to the data structure.
-   `double findMedian()` returns the median of all elements so far. Answers within `10-5` of the actual answer will be accepted.
  
### Solution
##### QuickSelect
- insert: O(1) - add to resizeable array
- findMedian: O(2N) - worst case, quickSelect 2 median element

##### Insertion sort using Binary Search
- Insert: O(N)
	- Assume array is sorted, we binary search for the next num position, pushh the rightward elements to the right to make space for new num element -> O(lgN + N) = O(N)
- findMedian: O(1) - just return element (n / 2)th 

##### Double Heaps

Maintain a maxHeap `lo` to store the first lower half and a minHeap `hi` to store the greater half such that the heaps are balanced are almost balanced (lower heap is always either equal or 1 element greater than the second heap)

If the 2 heaps are equal in size, median = `(lo.peek() + hi.peek())/ 2
else, median = `lo.peek()`

Insert: O(lgN) to insert and remove from heaps
findMedian: O(1) to access head of heaps

Space: O(N) to store all the data streams in heaps

```
Adding number 41
MaxHeap lo: [41]           // MaxHeap stores the largest value at the top (index 0)
MinHeap hi: []             // MinHeap stores the smallest value at the top (index 0)
Median is 41
=======================
Adding number 35
MaxHeap lo: [35]
MinHeap hi: [41]
Median is 38
=======================
Adding number 62
MaxHeap lo: [41, 35]
MinHeap hi: [62]
Median is 41
=======================
Adding number 4
MaxHeap lo: [35, 4]
MinHeap hi: [41, 62]
Median is 38
=======================
Adding number 97
MaxHeap lo: [41, 35, 4]
MinHeap hi: [62, 97]
Median is 41
=======================
Adding number 108
MaxHeap lo: [41, 35, 4]
MinHeap hi: [62, 97, 108]
Median is 51.5
```

```Java
class MedianFinder {
    // max heap
    PriorityQueue<Integer> lo = new PriorityQueue<>(Comparator.reverseOrder()); 
        
    // min heap
    PriorityQueue<Integer> hi = new PriorityQueue<>();
        
    public MedianFinder() {
        this.lo = new PriorityQueue<>(Comparator.reverseOrder()); 
        this.hi = new PriorityQueue<>(); 
    }
    
    public void addNum(int num) {
        // add the num to the correct PQ
        if (lo.isEmpty() || lo.peek() > num) {
            lo.add(num);
        } else {
            hi.add(num);
        }
        
        // balance PQ st 0 <= lo.size - hi.size <= 1
        if (lo.size() > hi.size() + 1) {
            hi.add(lo.remove());
        } else if (lo.size() < hi.size()) {
            lo.add(hi.remove());            
        }
    }
    
    public double findMedian() {
        int first = lo.peek();
        if (lo.size() == hi.size()) {
            int second = hi.peek();
            return (first + second) / 2.0;
        }
        return first / 1.0;
    }
}
```

##### AVL Binary SEARCH Tree
Harder to implement a self-balancing AVL tree on the spot in Java (None in Java Library)

Idea:
- Insert the elements in an AVL search trees - O(lgN)
- The median elements **is always either the root or one of its child or both*
- Adjust the pointers accordingly.
- Return the pointers when findMedian is called.

**Algorithm**

-   Two iterators/pointers `lo_median` and `hi_median`, which iterate over the `data` multiset.
    
-   While adding a number `num`, three cases arise:
    
    1.  The container is currently **empty.** Hence we simply insert `num` and set both pointers to point to this element.
        
    2.  The container currently holds an **odd** number of elements. This means that both the pointers currently point to the same element.
        
        -   If `num` is not equal to the current median element, then `num` goes on either side of it. Whichever side it goes, the size of that part increases and hence the corresponding pointer is updated. For example, if `num` is less than the median element, the size of the lesser half of input increases by 11 on inserting `num`. Thus it makes sense to decrement `lo_median`.
        -   If `num` is equal to the current median element, then the action taken is dependent on how `num` is inserted into `data`. **NOTE:** In our given C++ code example, `std::multiset::insert` inserts an element _after_ all elements of equal value. Hence we increment `hi_median`.
    3.  The container currently holds an **even** number of elements. This means that the pointers currently point to consecutive elements.
        
        -   If `num` is a number between both median elements, then `num` becomes the new median. Both pointers must point to it.
        -   Otherwise, `num` increases the size of either the lesser or higher half of the input. We update the pointers accordingly. It is important to remember that both the pointers _**must**_ point to the same element now.
-   Finding the median is easy! It is simply the **mean** of the elements pointed to by the two pointers `lo_median` and `hi_median`.