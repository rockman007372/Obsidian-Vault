## Decomposed FD

A [[Functional Dependency]] whose right-hand side consists of only **one** attribute.

ABC -> A, A -> E, ... are decomposed FDs.

## Non-trivial Decomposed FD

Decomposed FDs whose right-hand side does not have any attributes from the left-hand side.

- ABC -> A is trivial.
- ABC -> E is non-trivial.

## How to find non-trivial decomposed FD

Similar to finding key, through [[Closure]]

1. Compute the closure of **all** the subsets of attributes.
2. For each closure, remove the trivial attributes (attributes that appear in the left-hand side). 
3. Derive the decomposed FD (FDs with only one attribute on the right side)


Example: R(A, B, C) with A -> B, B -> A, B -> C

{A}+ = {A, B, C}
{B}+ = {A, B, C}
{C}+ = {C}
{A, B}+ = {A, B, C}
{A, C}+ = {A, B, C}
{B, C}+ = {A, B, C}
{A, B, C}+ = {A, B, C}

Non-trivial decomposed FDs are:
A -> B
A -> C
B -> A
B -> C
AB -> C
AC -> B
BC -> A






