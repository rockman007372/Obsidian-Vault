There are 2 types of problems:
- **Decision** problem: Is there a vertex cover of size $\leq k$?
- **Search** problem: what is the minimum vertex cover?

We claim Seach problem $\leq_{p}$ Decision problem.

Prove: If we have a solution to the decision problem, we can [[Binary Search]] for the Search problem in polynomial time - O(logN)