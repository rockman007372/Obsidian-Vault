A scalar subquery is a query that returns _at most a single value_ (i.e., a table with 1 row and 1 column).

Scalar subqueries are commonly used to perform calculations or comparisons based on *a single value* returned from a subquery.

Note:
- This is *dynamically checked* at run-time
- can be used as a *value* in queries
- If the result returns 0 row, then it is treated as `NULL`

![[Pasted image 20230220191935.png]]

Example:

```sql
-- Find all area, the pizza sold in the area, and all the prices of the pizza in that area.

SELECT (SELECT area
        FROM   Restaurants R
        WHERE  R.rname = S.rname),
       pizza, price
FROM   Sells S;

-- Equivalent to:

SELECT area, pizza, price
FROM Restaurant R JOIN Sells S
	ON R.rname = S.rname;
```

This can be useful when you want to display a calculated value for each row that depends on data from another table.

```sql
SELECT *
FROM   Sells
WHERE  price < (SELECT S.price -- Return a single constant value
                FROM   Sells S
                WHERE  rname = 'Corleone Corner'
                  AND  pizza = 'Margherita');
```

