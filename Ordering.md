## Single attribute ordering

```sql
-- Find all restaurants and their pizzas and prices sorted in descending order of price.
SELECT *
FROM   Sells
ORDER BY price DESC;
```

## Mutiple attribute ordering

```sql
--Find all pizza with recipes containing Cheese sorted in descending order of pizza and for each pizza sort in ascending order of ingredient.

SELECT *
FROM   Recipes
WHERE  pizza IN (SELECT pizza
				 FROM   Recipes
				 WHERE  ingredient = 'Cheese')
ORDER BY pizza DESC,     -- sort by pizza first
         ingredient ASC; -- then sort by ingre

-- This works because sorting is stable
```

## Limit and Offset

The `LIMIT` clause in SQL is used to limit the number of rows returned by a query. It can be useful when you only need to retrieve a certain number of rows, or when dealing with large datasets where it's not feasible to retrieve all the rows at once.

```sql
-- Find the 3 cheapest pizza, the restaurant selling them, and the price.
SELECT *
FROM   Sells
ORDER BY price ASC
LIMIT 3;
```

In addition to the `LIMIT` clause, you can also use the `OFFSET` clause to **skip a certain number of rows** before returning the results.

```sql
-- Find the "next" 3 cheapest pizza, the restaurant selling them, and the price.
SELECT *
FROM   Sells
ORDER BY price ASC
OFFSET 3 -- skip first 3 pizza
LIMIT  3;
```

>[!note]
> The order of `OFFSET` and `LIMIT` does not matter! You can apply limit first, then offset. This is similar to sliding a window of width 3 by 3 unit.