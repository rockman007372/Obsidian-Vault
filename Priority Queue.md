2022-06-23 14:59
Tags: [[Data Structure and Algorithm]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

## Language-specific Implementations
#### Java

```Java
// min heap
PriorityQueue<Integer> minHeap = new PriorityQueue<Integer>(); 

// max heap
PriorityQueue<Integer> maxHeap = 
	new PriorityQueue<>(Comparator.reverseOrder()); 
```

#### Python

```python
# importing "heapq" to implement heap queue
import heapq

# initializing list
li = [5, 7, 9, 1, 3]

# using heapify to convert list into heap
heapq.heapify(li)

# printing created heap
print("The created heap is : ", end="")
print(list(li))

# using heappush() to push elements into heap
# pushes 4
heapq.heappush(li, 4)

# printing modified heap
print("The modified heap after push is : ", end="")
print(list(li))

# using heappop() to pop smallest element
print("The popped and smallest element is : ", end="")
print(heapq.heappop(li))
```

## Definition

A PQ is an **abstract** data structure that provides a way to 
- store elements along with their associated priorities and 
- allows accessing and removing the element with the highest (or lowest) priority

It does not provide any implementation.

It is used in many [[SSSP]] algorithm. (Such as [[Dijkstra's Algorithm]])

![[Pasted image 20220623145902.png]]

## Implementations

#### Binary Heap 

![[Pasted image 20220623150048.png]]

See [[Heap]] for implementation details.

#### AVL Tree

All operations take O(lgN).

`extractMax` function can be reduced to O(1) by keeping a HashMap linking node to its position in AVL.