---
tags: toProcess
alias: 3NF
course: CS2102
type: content, lecture
date: 2023-04-18 Tuesday
---

### Overview
- Not as strict as [[Boyce-Codd Normal Form]]
- Small redundancy (not as small as [[Boyce-Codd Normal Form|BCNF]])
- Lossless join decomposition
- ! Ensures [[Dependency Preservation]] (preserve all FDs)

>[!definition]
> A table satisfies 3NF if and only if for every non-trivial decomposed FD:
> - Either the left hand side is a superkey
> - Or the right hand is a [[Prime Attributes|Prime Attribute]] (only **one** attribute since its decomposed FD) 

### Example

Table R(A, B, C). 
Non trivial and decomposed FDs: C -> B, AC -> B, AB -> C
Keys: AB, AC
C -> B is OK, since B is *a prime attribute* (part of key AB)
AC -> B is OK, since AC is a key of R
AB -> C is OK, since AB is a key of R

Hence R is in 3NF.

### Comparision between BCNF vs 3NF

- BCNF: every attribute must depend only on superkeys, no exception.
- 3NF: every attribute must depend only on superkeys, unless the attribute is a prime attribute itself.

Hence, 3NF is more lenient than BCNF:

>[!theorem]
> - R is in BCNF -> R in in 3NF
> - R is **not** in 3NF -> R is **not** in BCNF

### Related

[[3NF Decomposition]]