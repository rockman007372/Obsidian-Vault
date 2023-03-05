
```sql
WHERE <expr> <op> ANY <subquery>
```

Note:
- `ANY` returns `TRUE` if comparison evaluates to `TRUE` for _at least one_ row in the subquery `∃ row ∈ subquery : (<expr> <op> row) = TRUE`

Example:

```sql
-- Find all restaurants that sells any pizza cheaper than any pizza sold by Lorenzo Tavern (also possible, sells any pizza cheaper than the most expensive pizza sold by Lorenzo Tavern).

SELECT DISTINCT rname
FROM   Sells
WHERE  price < ANY (SELECT price
					FROM   Sells
					WHERE  rname = 'Lorenzo Tavern');
```