---
tags: 
aliases:
  - Minimal Cover
date: 2023-04-21 Friday
---
Finding the minimal cover/basis is an essential step in the process of normalization, especially when decomposing relations to higher normal forms.

### Definition

Let S be a set of FDs. **M** is a minimal basis of S if

1. M and S are **equivalent**: Every FD in S can be derived from M, and vice versa 
2. Every FD in M is a [[Nontrivial and Decomposed FD]]
3.  For any FD in M, if we remove an attribute from its LHS, then the FD cannot be derived from **S** (**no redundant attribute** on the LHS)
4. If any FD is removed from M, then some FD in S cannot be retrieved from M (**no redundant FD** in M)

### Example

$S = \{A → BD, AB → C, C → D, BC → D\}$

$M =  \{A → B, A → C, C → D\}$

To illustrate condition 3:
- Consider AB → C in S. If we remove B from the LHS, we have A → C. 
- A → C can be derived in S because $A^{+}= \set{A, B, C, D}$
- Hence B is redundant in AB→ C. The FD can be simplified to A → C.

### Algorithm to find minimal basis

> [!algorithm]
> 1.  Transform the FDs so that each right-hand side contains only one attribute (trivial decomposed FDs)
> 2. Remove redundant attributes on the LHS of each FD
> 3. Remove redundant FDs

Example: S = {A → BD, AB → C, C → D, BC → D}

**1. Transform to decomposed FDs**

S' = {A → B, A → D, AB → C, C → D, BC → D}

**2. Remove redundant attributes**

Check whether B is redundant in AB → C by checking the whether $A^+$ contains C. This includes the FD you are checking (AB → C in this case).

Since $A^{+}= \set{A, B, C, D}$, A → C can be derived. B is redundant.

Similarly, B is redundant in in BC → D since $C^{+}= \set{C, D}$.

Hence, S' = {A → B, A → D, A → C, C → D}

**3. Remove redundant FDs**

A → D can be derived from A → C and C → D, hence it is redundant.

Minimal basis M =  {A → B, A → C, C → D}


