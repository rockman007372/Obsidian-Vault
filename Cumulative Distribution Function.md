---
tags: 
aliases: 
---
Date:: 2022-09-12 Monday
Links: [[Random Variables, Distributions, Expectations]]
- - -


![[Pasted image 20220831144100.png]]

## c.d.f for Discrete RV

![[Pasted image 20220904142301.png]]

The c.d.f of a discrete RV is a **step function**: $F(X < 5) = F(X \leq 4)$
![[Pasted image 20220904142711.png]]

To calculate $P(a \leq X \leq b)$:
![[Pasted image 20220904142931.png]]

##### Examples
**Example 1: Convert p.m.f to c.d.f**

Let X = the number of heads of flipping 2 fair coins

Probability mass function of X:
![[Pasted image 20220904143142.png]]

$F(0) = P(X \leq 0) = f(0) + f(0-)= 1 / 4 + 0 = 1 / 4$

$F(1) = P(X \leq 1) = f(0) + f(1)= 3/4$

$F(2) = P(X \leq 2) = f(0) + f(1) + f(2) = 1$

We obtain the c.d.f:
![[Pasted image 20220904143820.png]]

**Example 2: Using the c.d.f above, derive the probability distribution function.**

Since F(x) **only has 4 values** and is also a **step function**, its distribution is a discrete distribution.

We obtain Rx = {0, 1, 2}. 

$f(0) = F(0) - F(0-) = 1 / 4$
$f(1) = F(1) - F(1-) = F(1) - F(0) = 3 / 4 - 1 / 4 = 1 / 2$
$f(2) = F(2) - F(2-) = F(2) - F(1) = 1 - 3 / 4 = 1 / 4$

**Example 3:**
![[Pasted image 20220904144729.png]]

![[Random Variables 2022-09-04 14.48.00.excalidraw]]

**Example 4:**
![[Pasted image 20220904145349.png]]

![[Pasted image 20220904145700.png]]

![[Random Variables 2022-09-04 14.57.39.excalidraw]]

**Example 5:**
![[Pasted image 20220904150550.png]]

**a) Suppose that board 1 and 2 are the only defectives in a lot of five. Define X = no. defective boards observed. Find the p.d of X**

![[Random Variables 2022-09-04 15.06.53.excalidraw||400]]

**b) Let F(x) be the c.d.f of X. Derive F(x)**
![[Pasted image 20220904151350.png]]

## c.d.f for Continuous RV
![[Pasted image 20220904151500.png]]
![[Pasted image 20220904151606.png]]

**Example:**



## Properties of C.D.F
1. No matter whether X is discrete or continuous, F(X) is **non-decreasing**  $$\forall x_1, x_2, \text{if }  x_1 < x_2, F(x_1) \leq F(x_2)$$
2. p.f and c.d.f are one-to-one correspondence → **Unique mapping**
3. The range of F(x) and f(x) must satisfy:
	- $0 \leq F(x) \leq 1$
	- For discrete distribution: $0 \leq f(x) \leq 1$
	- For continuous distribution, $f(x) > 0$ and can even be **greater than 1!!!** → $f(x)$ here is not probability.


