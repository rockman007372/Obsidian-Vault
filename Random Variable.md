---
tags: 
aliases: 
---
Date:: 2022-09-12 Monday
Links: [[Random Variables, Distributions, Expectations]]
- - -
# Random Variables
### **Definition**
Let S be the sample space for an experiment. 
Function X assigns a real number to every sample point s $\in$ S
 - X is a **random variable** 
 - X : S → $R_x$ 
 - $R_x$ is the range of function S

### **Example**
- S = sample space of throwing 2 fair coins
- S = {HH, HT, TH, TT}
- X = number of heads 
- $R_{x}$ = {0, 1, 2}
- X(HH) = 2
- X(HT) = 1

The set {X = x} is a subset of S:
- {X = 2} = {HH}
- {X = 1} = {HT, TH}
- {X <= 1} = {TT, HT, TH}

This gives P(X = x) and P(X $\in$ A):
- P(X = 0) = P(TT) = 1 / 4
- P(X <= 1) = 3 / 4 