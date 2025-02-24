### Basic Idea

If problem A can be reduced to problem B in polynomial time,  it means **any** instance of A can be reduced to an instance of B. 

![[Pasted image 20231106164703.png]]

If A can be reduced to B polynomially, and we can solve B in polynomial time, we can also solve A in polynomial time.

Notation: $A \leq_p B$ 
- This means A is polynomially reducible to B. 
- It also means problem B is "harder" than A (the hardest problem in A is at most as hard as B)

If $A \leq_p B$  and $B \leq_p A$, we say they are equivalent, or $A \equiv_p B$ 

### Applications

1. We use reductions to find algorithms to solve problems. 
2. We also use reductions to show that we can’t find algorithms for some problems. (e.g. an NP-hard problem can be reduced to this problem)

---
[[Basic Reduction Strategies]]
[[Self-Reducibility]]

