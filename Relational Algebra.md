---
tags: processed
course: CS2102
type: lecture
date: 2023-01-23 Monday
---


## Relational Algebra

### Introduction

- Operands: Relations / variables representing relations
- Operators: Transformation from one or more input relations into **one** output relation
- Unary Operators: selection, projection, renaming
- Binary Operators: cross product, union, intersection, difference
- Why: For query optimization → dont care in CS2102

![[Pasted image 20230123150449.png]]

### Closure Property

>[!definition]
> A set of values is closed under the set of operators if any combinations of the operators produce only values in the given set.

Eg:
- $Z^{+}$ is closed under $\set{+}$ but not under $\set{+, -}$

> [!Theorem]
> Relations are closed under Relational Algebra. 

Implication:
- We can **chain operations** because all input and outputs are relations.

![[Pasted image 20230123150913.png]]

## Three-Valued Logic

Consist of True, False, NULL.

### Logic Table

![[Pasted image 20230123151253.png]]


![[Pasted image 20230123151305.png]]

### Operations on NULL

- Any relational/arithmetic operation with NULL produces NULL values.
- We add operators to treat NULL as values: EQUIVALENT

![[Pasted image 20230124154817.png]]

## Basic Operators

### Selection

![[Pasted image 20230123152156.png ]]

- Equivalent of `filter` function.
- Result table has same schema but less than or equal number of rows.

![[Pasted image 20230123153031.png]]

### Projection

![[Pasted image 20230123152748.png]]

- Projection keeps on the **columns** specified in the ordered list $l$ and in the same order.
- ! The number of rows may be smaller because relation is defined as a set of tuples → Rows must be unique! Hence duplicated rows are removed.

![[Pasted image 20230123153007.png]]

### Renaming

- Rename the attributes of the input
- Relevant for set and join operations

![[Pasted image 20230123153847.png]]

## Set Operators

### Union Compatibility

>[!Definition]
> Two relation R and S are union-compatible if it satisfies both of the following:
> - R and S have the same number of attributes
> - The corresponding attributes have the same or compatible domains

- Just because 2 relations are union-compatible, does not mean the set operation is meaningful.
- Example of union-compatible relations:

```sql
Employees(name: TEXT. role: TEXT, age: INT)
Teams(ename: TEXT, pname: TEXT, hours: INT)
```

### Cross Product

![[Pasted image 20230123154738.png]]

>[!definition]
> The cross product of 2 relations (R x S) is a relation formed by combining all pairs of tuples from the 2 input relations.

- The set of attributes in R and S must be **disjoint**: $$Attr(R) \cap Attr(S) = \emptyset$$
>[!example]
> Find all pairs of senior employee names (age >= 45) and junior employee names (age <= 25) 

![[Pasted image 20230123155749.png]]

**Observation:**
-   Given two relations _R_ and _S_, the size of the cross product is |_R_| × |_S_|
-   In practice, many to most queries requiring a cross product _also_ require
    -   Selection operation to remove unnecessary rows
    -   Projection to remove unnecessary/duplicate columns (optional)


## Join Operators

- Simplify relational algebra expression by combining cross product, selection and (optionally) projection.
- Avoid generating all |R| x |S| intermediate tuples.
- Base type: For each element in R, combine with each element in S

![[Pasted image 20230123161148.png]]

### Inner Join

- Includes only tuples that satisfy the condition.
- Consists of:
	- $\theta$-Join $\Join_{theta}$
	- Equi-Join $\Join_{=}$
	- Natural Join $\Join$

#### Theta Join 

$$R \Join_{theta} S = \sigma_{[\theta]}(R \times S)$$

> [!example]
> For all the projects, find the offices of the managers.

$$Projects ⋈[manager=mname]
(ρ[mname←name](Managers))$$
#### Equi Join

$$R \Join_{=}S$$
- A special θ-join where the only relational operator that can be used is equality (e.g., = or ≡)
- Can yse arbitrary relational operator (=, <, >, <>, ...)
- ? Most common Inner Join operation, especially when performing inner join following foreign key constraints

#### Natural Join

$$ R \Join S = \pi_{[l]}(R \Join_{[\theta]}S)$$
where:
- $l = Attr(R) \cup (Attr(S) - Attr(R)) =  Attr(R) \cup Attr(S)$
- $\theta = \forall A_{i} \in Attr(R) \cap Attr(S): R.A_{i}= S.A_i$

**In other words:**
- The join is performed over all **common attributes** btw R and S such that:
	- We only combine if the value of the common attributes are equals
	- ? The output relations contains the common attribute of R and S **only once**

**Example**
Find the office of the manager in charge of each project.

![[Pasted image 20230123171133.png]]

- We rename attribute `Managers.name` to `Managers.manager` to match the name of the attribute `Project.manager`
- Natural join will check the the common attribute `manager` and perform cross product only if the attribute values are the same (eg. `manager == Judy`)

### Outer Join

- Also include tupples that do not satisfy the condition.
- Why? Sometimes a tuple in R or S that do not match are also of interest (dangling tuple)

**Informal Steps**
1. Perform inner join M = R $\Join$ S
2. Add dangling tuples from M from:
	- R in case of a **left** outer join - ⟕
	- S in case of a **right** oter join -  ⟖
	- R and S in case of a **full** outer join - ⟗
3. Pad missing attribute values of dangling tuples with NULL.

**Examples**

Find all the employees not assigned to any project

![[Pasted image 20230123164446.png]]

- The dangle tuples are those where employees' names do not match ename.
- In those tuples, the ename will be assigned NULL.
- ! Pay attention to which relation comes first.






## Complex Expressions

Motivation: Different query trees can produce the same relational output.

### Equivalence

> [!definition]
> Expressions Q1 and Q2 are:
> - **Strongly** equivalent if they both produce error **or** both produce the same result.
> - **Weakly** equivalent **if** there is no error **then** they both produce the same result.

![[Pasted image 20230123171823.png]]

![[Pasted image 20230123171842.png]]

Observation:
- In weak equivalence, almost everything is equivalent except for non-commutativity of Cross Product and Join
- Anything with an 'if' will be equivalent in weak equivalence.

## Summary
![[Pasted image 20230123170310.png]]

## Questions/Cues

- More examples of natural join? When to use natural join?
## Data

Data used in this lecture:

![[Pasted image 20230123164644.png]]



---
Links: [[CS2102]]