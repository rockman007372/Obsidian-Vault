
```sql
WHERE <expr> <op> ALL <subquery>;
```

Note:
- Returns a row in the outer table if all comparison operations are true: `∀ row ∈ subquery : (<expr> <op> row) = TRUE`

Example:

```sql
-- Find all restaurants that sells any pizza more expensive than all pizzas sold by Mammas Place (also possible, sells any pizza more expensive than the most expensive pizza sold by ...).

SELECT DISTINCT rname
FROM   Sells
WHERE  price > ALL (SELECT price 
					FROM   Sells 
					WHERE  rname = 'Mammas Place');
```


```sql
-- Find the most expensive pizza sold by each restaurant
SELECT *
FROM   Sells S1
WHERE  S1.price >= ALL
  (SELECT S2.price
   FROM   Sells S2
   WHERE  S2.rname = S1.rname);

-- Can also use GROUP BY and aggregation function MAX
SELECT *
FROM   Sells 
GROUP BY rname
HAVING price = MAX(price)

```
