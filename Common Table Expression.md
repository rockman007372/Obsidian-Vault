## Motivation

You want to create a table on the go and refer to it in the `FROM` clause.

```sql
-- find the 3 cheapest pizzas and order them in descending order
SELECT * 
FROM ( SELECT * FROM Sells ORDER BY price ASC LIMIT 3 ) T1 
ORDER BY price DESC;
```

You can bring T1 out by creating a Common Table Expression (CTE).

## CTE

CTEs are like "temporary" table, but no actual tables are created. CTEs help to improve readability, debugging, and maintenance.

Syntax:

```sql
WITH 
	CTE_1 AS ( Q_1 ), 
	CTE_2 AS ( Q_2 ), 
		⁝, 
	CTE_n AS ( Q_n ) 

-- main SELECT statement
Q_0 
```

Note:
- Each CTE_i is the name of a temporary table defined by query Q_i
- Each CTE_i can reference any other CTE_j that has been declared **before** CTE_i (i.e., j < i)

## Example

>[!question]
> For each pizza with Cheese as one of its ingredient, find the restaurant names that sells it and the customer names that likes it such that the customer and restaurant are in the same area

```sql
WITH 
	PizzaWithCheese (pizza) AS ( 
		SELECT DISTINCT pizza 
		FROM Recipes 
		WHERE ingredient = 'Cheese' 
	), 
	RestaurantWithCheese (rname, pizza, area) AS ( 
		SELECT DISTINCT rname, pizza, area 
		FROM Sells NATURAL JOIN Restaurants -- join to get area
		WHERE pizza IN ( SELECT * FROM PizzaWithCheese ) 
	), 
	CustomerLikesCheese (cname, pizza, area) AS ( 
		SELECT DISTINCT cname, pizza, area 
		FROM Likes NATURAL JOIN Customers -- join to get area
		WHERE pizza IN ( SELECT * FROM PizzaWithCheese ) 
	) 
	
SELECT pizza, rname, cname 
FROM RestaurantWithCheese NATURAL JOIN CustomerLikesCheese;
-- join on pizza and area
```