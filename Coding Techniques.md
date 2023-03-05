2022-06-28 00:05
Tags: [[TIPS]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

![[Pasted image 20220612121538.png]]

## Part 1: Proactive Communication

1. Listen carefully (keywords, all info are useful, no excessive info)
2. Ask Questions
   + clarify inputs: Ask questions based on data structure of input (array, lists, trees...)
   + clarify outputs: what is expected
   + clarify constraints (size of array, length of characters...)
   + validate assumptions
3. Draw examples (test cases): not too large or too smalls, just simple ones
   + You can draw simple diagrams and pointers:

```python
[1, 2, 3] # list

       hi
       v
(1, 2, 3) # tuple with pointer
 ^
 lo


{"apple" : 1, "orange" : 2} # dictionary

1 -> 2 -> 3 # Linked List

	    # tree
		  6 
	4			7
1		5	6	 	8		 
```

## Part 2: Design algorithm 

1. **Brute force** solution: rmb to state time/space complexity
   
2. **Optimize** solution:
   + General tips: unused info, fresh example, solve it incorrectly first, trade space for time, precompute info (any overlapping substructures?), hash table (very common)
   + BUD: 
      + Bottleneck: runtime is capped at some step
      + Unnecessary Work: extra steps? Can terminate early?
      + Duplicated Work: doing the same thing?
   + DIY: how would you solve it in real life
   + Simplify and generalize: break into simpler cases, then generalize 
   + Base case and build: recursion
   + Data Structure brainstorming: going through all known data structures

3. Create **Scaffold** / Structure before coding.

   ![[Pasted image 20220618170525.png]]
   
4. Discuss complexities and trade-offs at every step.

#### Part 3: Debug
Things to check for:
+ off-by-ones
+ variable names
+ brackets
+ adding vs substracting
+ min vs max

Testing codes: 
+ Always test code MANUALLY without being prompted
+ Choose suitable test cases:
	+ Edge cases: at least 2
	+ Suitable example size (Not too large or small)
+ Copy paste the examples you came up with in the beginning
+ Use pointers for visualisation
+ Keep track of key variables