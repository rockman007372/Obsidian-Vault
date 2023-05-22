Motivations:
- Only some parts of the table are of interest
- Not all parts of the table should be accessible to users
- The same table queries are frequently used.

We need to represent these parts of the table in some form of **external schemas**. These external schemas are called View.

- Views are virtual tables. They are permanently-named queries that may be computed everytime the virtual table is accessed. 
- Views can be used like a normal table, but there are **restrictions**.

Example: Assuming finding pizza with cheese is a frequent query

```sql
CREATE VIEW PizzaWithCheese (pizza) AS 
	SELECT DISTINCT pizza 
	FROM Recipes 
	WHERE ingredient = 'Cheese';
```

