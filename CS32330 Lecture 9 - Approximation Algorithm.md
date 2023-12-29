---
tags:
  - toProcess
course: CS3230
type: lecture
date: 2023-11-13 Monday
---

Motivation:
- If we know a problem is NP-hard, instead of coming with a potentially non-existent poly-time optimal solution, we can just "approximate" the solution so that it is as close to optimal as possible.

p-approximation algorithm:
- runs in polytime
- solve any arbitrary instance of the problem
- find solution within ratio p of true optimum

Let OTP(X) denotes the optimal solution, and A(X) denotes the approximate solution for all input X. A is a p-approximation algorithm iff $$max(\frac{OTP(X)}{A(X)}, \frac{A(X)}{OTP(X)}) \leq p$$
First clause if for maximization problem, second clause is for minimization problem.

Tip to proving the algorithm A satisfies some approximation ratio is to **find a function f(X)** such that 
- f(X) provides a **lower bound for the optimal solution** OTP(X)
- f(X) provides an **upper bound for the approximate solution** A(X)


## Problems covered

- Load Balancing
- Center Selection
- Integer Programming? Weighted Vertex Cover?