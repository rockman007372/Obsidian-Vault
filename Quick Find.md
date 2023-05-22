Quick-Find is a naive implementation of [[Union-Find]].

Idea: Each object has a **component identifier** (to identify which component the object belongs to)

## Find

Find(a, b): Check if object a and b have the same component id.
  
![[Pasted image 20220616143245.png||600]]

## Union

Union(p, q): 
- go through the `component id` array
- update the objects with the to-be-updated `component id` to the `target id`

![[Pasted image 20220616143352.png||600]]

## Time complexity

+ Find operation: O(1)
+ Union operation: O(n)