---
tags: []
course: CS3230
type: lecture
date: 2023-08-22 Tuesday
---
## Tips

- Log grows slower than polynomial and polynomial grows slower than exponential
- ! Apply $x = e^{lg(x)}$ to [compare OOG](https://math.stackexchange.com/questions/1935285/order-of-growth-for-algorithms-n-logn-vs-2n)
- Apply L'Hospital Rule: 

![[Pasted image 20230903101738.png]]
- Use transitivity, symmetry and additivity to compare OOG:
	- Transitivity: $$f = \theta (g) \text{ and } g=\theta (h) \Rightarrow f = \theta (h) $$
	- Symmetry: $$f = \theta (g) \iff g = \theta (f)$$
	- Additive: $$f = \theta (h) \text{ and } g=\theta (h) \Rightarrow f + g = \theta (h) $$
## Content
### Word-RAM model

How does an instruction execute:
1. decode ins
2. fetch operands to processor
3. processor execute ins
4. return result to ram

- word is the basic storage of RAM

### How to measure running time

Mathematically: number of instructions taken in Word-RAM model.

### Example: Fibonacci Number

- F(0) = 0
- F(1) = 1
- F(n) = F(n - 1) + F(n - 2) for n > 1

Problem 1: Given a and b, find F(n) mod m
- Recursive
- Iterative: 2 variables, dp solution
- If we analyze run time, recursive is exponential while iterative is linear (since its dynamically computed)

### Polynomial Time

Exponential time: O(2^n)
- Bruteforce solution, check every combination

**Desirable scaling property**: when input size doubles, the algo slow down by some constant factor C

An algorithm is poly-time if:

>[!definition]
> There exists constant c > 0 and d > 0 st on every input of size N, its running time is bounded by cN^d steps.

### Worst-Case Analysis

Worst case running time:
- Obtain bound on **largest possible running time** of algorithm on input of a given size N
- Too draconian, but effective generally

Average case runnning time:
- Obtain bound on running time on **random** input as a function of input size N
- Hard to accurately model by random distributions
- Algo tuned for a certain distribution may perform poorly for other inputs

> [!theorem]
> An algo is efficient if its running time is polynomial
### Asymptotic Order of Growth

compare efficiency of 2 algo:
- T(n) = 10n + 1000
- T(n) = n^2 + 1000
- algo 2 is more efficient when n < 10
- but for asymptotically large input, algo 1 is always more efficient

Refresher:
- Upper bound: Big O
- Lower bound: Big omega
- Tight boung: Big tether

Properties:
- Transitivity
- Additivity: if f = O(h) and g = O(h) then f + g = O(h)


Common function observations:
- Logarithms: for every x > 0, log N = O(N^x) => **log grows slower than every polynomial**
- Exponentials: for every r > 1 and d > 0, N^d = O(r ^ N) => **exponential grows faster than poly**







---
Links:
