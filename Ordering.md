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

```sql
-- Find the 3 cheapest pizza, the restaurant selling them, and the price.
SELECT *
FROM   Sells
ORDER BY price ASC
LIMIT 3;

-- Find the "next" 3 cheapest pizza, the restaurant selling them, and the price.
SELECT *
FROM   Sells
ORDER BY price ASC
OFFSET 3 -- skip first 3 pizza
LIMIT  3;
```