
- [[Subqueries]]
- [[Scalar Subqueries]]
- [[Scoping Rule in Composed Queries]]
- [[Multiple Nested Subqueries]]
- [[Equivalent Subquery Commands]]

## Remarks

1. Difference in behaviour of `ANY` vs `ALL` when subquery returns empty table:
- The subquery in an `ANY` command returns an empty table, the result will be **false** for any comparison operator.
- If the subquery in an `ALL` command returns an empty table, the result will be **true** for any comparison operator
2. Be careful of scoping - cannot access the table inside subquery from outside!
3. Queries can return table with **duplicated columns**, unlike [[Relational Algebra]]

