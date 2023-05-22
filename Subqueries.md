- Subqueries are queries within another queries
	- Can appear in SELECT/FROM/WHERE clause
- Can be used to construct complex queries.
- Subqueries expressions:
	- [[IN Subqueries]]
	- [[EXISTS Subqueries]]
	- [[ANY Subqueries]]
	- [[ALL Subqueries]]

## Note

1. Difference in behaviour of `ANY` vs `ALL` when subquery returns empty table:
- If the subquery in an `ANY` command returns an empty table, the result will be **false** for any comparison operator.
- If the subquery in an `ALL` command returns an empty table, the result will be **true** for any comparison operator (vacuously true)