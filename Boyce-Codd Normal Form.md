---
alias: BCNF
---

> [!definition]
> A table R is in BCNF if every [[Nontrivial and Decomposed FD]] has a [[Superkey]] as its left-hand side.

 
### Example

Given a table R(A, B, C), and A → B, B → A, B → C. 

1. Check closure of each subset: 
- A+ = ABC
- B+ = ABC
- C+ = C
- AB+ = ABC
- AC+ = ABC
- BC+ = ABC
2. Find the non-trivial decomposed FDs: 
- A → B
- A → C
- B → A
- B → C
- AB → C
- AC → B
- BC → A
3. Keys of R = A, B

Since **the left side of all the FDs are superkeys**, R is in BCNF.

## Key topics

- Motivation: [[Why is BCNF desireable]] 
- Validation: [[How to check if a table is in BCNF]]
- Decomposition Algorithm: [[BCNF Decomposition]] 
- Properties: [[Properties of BCNF]]








