A monotonic stack is a stack whose elements are always sorted. 

Let's say we want a monotonic **increasing** stack, i.e. the elements in the stack are always sorted in ascending order. To maintain this monotonic stack, we need to make sure that whenever we push a new element, it is the largest value in the stack. 

Before we push an element `num`, we check the top of the stack. If the top of the stack is greater than `num`, we pop from it. Since there may be multiple elements greater than `num` in the stack, we need to use a while loop to "clean" the stack before pushing `num`.

Only once there are no elements in the stack greater than `num` will we push `num`.

##### Use case
- Helpful in reduce time complexity to O(1) amortized cost.