
```sql
WHERE <expr> [NOT] IN [ <subquery> | <tuple> ];
```

Note:
- If `<expr>` is a single attribute/column, the subquery **must** return exactly one column as well.
- `IN` returns TRUE if `∃ row ∈ <subquery> : (row = <expr>) = TRUE`
- `NOT IN` returns TRUE if `∀ row ∈ <subquery> : (row <> <expr>) = TRUE`

Example:

```sql
-- subquery
SELECT DISTINCT rname
FROM   Sells
WHERE  pizza IN (SELECT pizza -- one single attribute
				 FROM   Recipes
				 WHERE  ingredient = 'Cheese');

SELECT cname, area
FROM   Customers
WHERE  cname NOT IN (SELECT cname
					 FROM   Likes);
```

```sql
-- explicit tuple
SELECT *
FROM products
WHERE product_id IN (101, 102, 103);
```

```sql
-- multiple columns in expression
SELECT *
FROM products
WHERE (product_id, size) IN (SELECT product_id, size 
							 FROM inventory 
							 WHERE quantity > 0);
```
