---
tags: LeetCode, leetcode
topics: 
difficulty: medium
performance: uncomplete
date: 2023-06-11 Sunday
---

## Questions

 Design a Data Structure `SpecialStack` that supports all the stack operations like `push()`, `pop()` and an additional operation `getMin()` which should return minimum element from the SpecialStack. 
 
 All these operations of SpecialStack must be `O(1)`.

## Solution

### 2 stacks 

Idea:
- First stack stores the actual elements pushed into the stacks.
- Second stack stores the current minumum element at **any** point in the stack.

Example:
- Assume we push a value x to the first stack. Let y be the top value of the second stack, which is also the minimum value in the first stack at the point before pushing x. If x < y, push x to the 2nd stack. Else, push y (again) to the 2nd stack.
- Pop operations require popping both stacks. 

Time: O(1) for all operations
Space: O(N) for the auxilary stack.

### 1 stack and 1 variable 

Idea:
- We can reduce space complexity further to O(1), using **math**. 
- The variable still keeps the smallest element at any point. 
- However, the stack does not contain the actual elements in the stack, but a **transformed value** derived from the value pushed and the current smallest value at that point. This allows us to later derive both these values after a pop operation.

**Push(x):** Insert x at the top of the stack

- If the stack is empty, insert x into the stack and make `minEle` equal to x.
- If the stack is not empty, compare x with minEle. Two cases arise:
    - If x is greater than or equal to minEle, simply insert x.
    - If x is less than minEle, insert `2x – minEle` into the stack and make `minEle` equal to x.

**Pop():** Removes an element from the top of the stack

- Remove the element from the top. Let the removed element be y. Two cases arise:
    - If y is greater than or equal to minEle, the minimum element in the stack is still minEle.
    - If y is less than minEle, the minimum element now becomes `(2 * minEle – y)`, so update `minEle = 2minEle – y`. This is where we retrieve the previous minimum from the current minimum and its value in the stack.

>[!Important Points] 
> - Stack doesn’t hold the actual value of an element if it is minimum so far.
> - The actual minimum element is always stored in the minEle variable

Why does this work? After a pop operation, we can detect if the min value of the stack changed if the pop value is smaller than the current `minEle`. We can prove this invariant:

```
Let the value pushed be x. Assuming x is less than the current minEle:

x < minEle 
x - minEle < 0
x - minEle + x < x
2x - minEle < x

After this iteration, new minEle = x. The value pushed into the stack is (2x - minEle).

Later, when (2x - minEle) is popped, it is guaranteed to be smaller than the current minEle. This triggers us to update the minEle and retrieve the actual element popped.
```



---
Link: [[LeetCode]]
