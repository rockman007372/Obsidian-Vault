---
tags: LeetCode, datastructure
aliases: 
topics: queue, stack
difficulty: easy
performance: complete, onTime
---
Date:: 2022-07-24 Sunday
Tags: [[LeetCode]] - [[Armotized Analysis]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Implement Queue using 2 Stacks
### My Performance
#complete #onTime 

### Questions
Difficulty: #easy
Implement a queue using 2 stacks 

### Solution

Push: O(1)

Pop: O(1) armotized cost!
- After N pushes, first pop operation costs O(2N)
- Afterwards, each pop operation costs O(1)
- N pushes followed by N pops must have been done before the pop operation becomes expensive again.
- Hence, using armotized cost analysis: cost = $\frac{O(N) + O(2N) + O(N)}{O(2N)}$ = $O(1)$

Peek: O(1) - cache the first value in the queue.

```Java
class MyQueue {
    private Stack<Integer> stackOne;
    private Stack<Integer> stackTwo;
    private int front;
        
    public MyQueue() {
        this.stackOne = new Stack<>();
        this.stackTwo = new Stack<>();
    }
    
    public void push(int x) {
        // We push into the first stack
        if (stackOne.isEmpty()) {
            this.front = x;
        }
        this.stackOne.push(x);
    }
    
    
    public int pop() {
        // If 2nd stack is not empty, just pop
        if (!stackTwo.isEmpty()) {
            return stackTwo.pop();
        }
        
        // else, we pop all elements in stack 1 and 
        // add them to stack 2, then we pop stack 2
        while (!stackOne.isEmpty()) {
            stackTwo.push(stackOne.pop());
        }
        return stackTwo.pop();
    }
    
    public int peek() {
        if (!stackTwo.isEmpty()) {
            return stackTwo.peek();
        }
        // cache first value in queue first 
        // stack is empty
        return this.front;
    }
    
    public boolean empty() {
        return stackOne.isEmpty() && stackTwo.isEmpty();
    }
}
```
