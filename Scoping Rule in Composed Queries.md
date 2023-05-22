>[!Rule]
> - A table alias declared in a (sub-)query Q can **only** be used in Q or subqueries nested within Q
> - If the same table alias is declared in both subquery $Q_1$ and in outer query $Q_0$ (or not at all), the declaration in $Q_1$ is applied

**General Rule:**
- From inner to outer queries in case of multiple nestings.
- Cannot access alias of inner subqueries from outer queries. In other word, a subquery can access data from tables in the outer query, but the outer query cannot access data from tables in the subquery.

Example:

```sql
SELECT 
	(SELECT area 
	FROM Restaurants R 
	WHERE R.rname = S.rname), pizza, price 
FROM Sells S;
```

- Alias S can be accessed by in inner subquery, but outer subquery **cannot** access alias R