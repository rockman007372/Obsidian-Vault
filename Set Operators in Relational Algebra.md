
## Union Compatibility

[[Union Compatible]]

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

## Cross Product

![[Pasted image 20230123154738.png]]

>[!definition]
> The cross product of 2 relations (R x S) is a relation formed by combining all pairs of tuples from the 2 input relations.

- The set of attributes in R and S must be **disjoint** (so there is no duplicated attribute in result): $$Attr(R) \cap Attr(S) = \emptyset$$
>[!example]
> Find all pairs of senior employee names (age >= 45) and junior employee names (age <= 25) 

![[Pasted image 20230123155749.png]]

**Observation:**
-   Given two relations _R_ and _S_, the size of the cross product is |_R_| × |_S_|
-   In practice, many to most queries requiring a cross product _also_ require
    -   Selection operation to remove unnecessary rows
    -   Projection to remove unnecessary/duplicate columns (optional)