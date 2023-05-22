2022-06-09 17:57
Tags: {{[[Data Structure and Algorithm]]}}  
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

### Main Points
Subset of [[Dynamic Programming]] problems, but solution is quite different from [[Tabulation]] and [[Memoization]] approach.

Usually contains 2 pointers, one indicating the beginning of the window, one for the end of the window.

A window represents the current section of the array/string you are looking at, and there will usually be constants to store current information.

### Clues: 
+ ordered and iterable data structure like array or string
+ looking for subrange (longest/ shortest/ target value)
+ apparent naive or brute force solution in O(N^2)

### Types of Sliding Window
1. [[Fast-Slow Sliding Window]]
2. [[Fast-Catch Up Sliding Window]]
3. [[Fast-Trailing Sliding Window]] 
4. [[Front-Back Sliding Window]] 