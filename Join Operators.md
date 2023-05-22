
- Simplify relational algebra expression by combining cross product, selection and (optionally) projection.
- Avoid generating all |R| x |S| intermediate tuples.
- Base type: For each element in R, combine with each element in S based on the condition set.

![[Pasted image 20230123161148.png]]

## Types of Joins Operations

- [[Inner Join]]
- [[Outer Join]]

> [!attention]
> Notice the difference:
> - If there are no common attributes, the join behaves as a Cartesian product.
> - If there are common attributes, but no values are equal, the result is an empty table!