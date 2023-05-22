>[!Definition]
> Let S be the given set of FDs on the original table and S' be the set of FDs on the **decomposed** tables.
> 
> The decomposition preserves all FDs $\iff$ S and S' are equivalent:
> - Every FD in S' can be derived from S
> - Every FD in S can be derived from S'

Example:

S = {A -> C, AC -> D, E -> AD, E -> H}
S' = {A -> CD, E -> AH}

Use **closure** to prove that they are equivalent!

Prove S' can be derived from S:
{A}+ = {A, C, D} => A -> CD
{E}+ = {E, H, A, D} => E -> AH

And vice versa, prove S can be derived from S'...

## What is the point of preserving FDs?

>[!Why?]
>Easier to avoid "inappropriate updates".

Table R(A, B, C) with AB -> C and C -> B

![[Pasted image 20230421132722.png]]

Keys = {AB}, {AC}

BCNF decomposition: 

- R1(A, C)
- R2(B, C) 

In the original table, AB -> C, hence these 2 tuples violate the dependency: 
(a1, b1, c1) and (a1, b1, c2)

But since we store A and B separately in R1 and R2, its difficult to check if these 2 tuples exist at the same time. For example, if someone wants to insert (a1, b1, c2), its not easy to check whether (a1, b1, c1) already exists. 

The dependency loss when we decompose tables make insertion/update difficult.