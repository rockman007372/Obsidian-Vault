2022-08-01 00:54
Tags: [[Permutation]] - [[Combination]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Navigating Grid using Combinations and Permutations
### Main Points
![[Pasted image 20220801005410.png]]

Suppose we're on a 4 × 6 grid. We can only traverse up and right (no backtracking). How many ways can we traverse the grid?

We can view the ups and downs as following and find the different ways to arrange them:

> r r r r r r u u u u

Hence we can solve this in various ways:
1. $\frac{10!}{6! * 4!}$ 
2. $10C4$