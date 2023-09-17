
```sql
SELECT [ DISTINCT ] <target-list> -- Projection of selected attributes
FROM <relation-list> -- Cross products of relevant relations 
WHERE <conditions> -- Based on principle of acceptance
```

>[!Principle of Acceptance]
>Perform the operation if the condition evaluates to **True**. 

## SQL to Relational Algebra

```SQL
SELECT DISTINCT a1, a2, ..., am
FROM r1, r2, ..., rn
WHERE c
```

is equivalent to:

```
π[a1, a2, ..., am](σ[c](r1 × r2 × ... × rn))
```

Only remove duplicated rows if `DISTINCT` is specified.

## SELECT clause

- Combine and process attribute values
- Rename columns
- Remove duplicated rows

```sql
SELECT rname, pizza, 'S$' || (price * 1.36) AS sgd 
FROM   Sells;

SELECT DISTINCT pizza -- remove duplicates
FROM   Sells;
```

Note:
- `DISTINCT` keyword checks for distinct rows using `IS DISTINCT FROM`, hence duplicated `NULL` values are reduce to one `NULL` value.

## WHERE clause

Note:
- To find tuples with `NULL` values, use `IS NULL` or `IS NOT NULL` due to principle of acceptance.

```sql
SELECT cname
FROM   Customers
WHERE  area IS NULL; -- Not area = NULL
```

- Pattern Matching for String: 
	- `_` matches any **single** character
	- `%` matches any sequece of **0 or more** more characters

```sql
SELECT pizza
FROM   Pizzas
WHERE  pizza LIKE 'Ma%a'; -- matches any sequence of 0 or more chars
```

![[Pasted image 20230220162557.png]]

## Set Operations

>[!TIP]
> Use set operations to **decompose** the problem into smaller problem!

Let Q1 and Q2 be two SQL queries that yield [[Union Compatible]] tables:
-   `Q1 UNION Q2`   =   Q1 ∪ Q2
-   `Q1 INTERSECT Q2`   =   Q1 ∩ Q2
-   `Q1 EXCEPT Q2`  =   Q1 − Q2

Note:
- ! Eliminate duplicated rows by default
- Column names follow the left relation
- The ordering of output may be different (dependent of relational algebra?)

What if you want to keep duplicates? Use the `ALL` keyword:

```sql
Q1 UNION ALL Q2
Q1 INTERSECT ALL Q2
Q1 EXCEPT ALL Q2
```

Note:
- This may lead to unintuitive result:

```SQL
Q1 = {1, 2, 2}
Q2 = {2, 3}

Q1 UNION ALL Q2 = {1, 2, 2, 2, 3}
Q1 INTERSECT ALL Q2 = {2}
Q1 EXCEPT ALL Q2 = {1, 2}
```

- Basically, each element is treated as a distinct element. 

## Join Operations

A table name can only appear at most once in the FROM clause, unless we rename it:

```sql
-- Error
SELECT rname, rname
FROM   Restaurants, Restaurants
WHERE  rname < rname
  AND  area = area;

-- No Error
SELECT r1.rname, r2.rname
FROM   Restaurants AS r1, Restaurants r2
WHERE  r1.rname < r2.rname
  AND  r1.area = r2.area;
```

To apply [[Inner Join]], we use `JOIN` operation with command `ON` to specify condition:

```sql

-- For all pizzas with cheese, find the restaurant that sells the pizza and the price of the pizza
SELECT DISTINCT rname, price
FROM   Sells S JOIN Recipes R -- Equi-Join
    ON S.pizza = R.pizza
WHERE  R.ingredient = 'Cheese';

--equivalent to:
SELECT DISTINCT rname, price
FROM   Sells S, Recipes R
WHERE  S.pizza = R.pizza
  AND  R.ingredient = 'Cheese';
```

We can make use of **Universal schema assumption** (same attributes have the same name) and `NATURAL JOIN`:

```sql
SELECT DISTINCT rname, price
FROM   Sells S NATURAL JOIN Recipes R -- no need S.pizza = R.pizza
WHERE  R.ingredient = 'Cheese';
```

To get the **dangling tuples**, we use [[Outer Join]]:

```sql

-- Find all customer names that does not like any pizza.

SELECT DISTINCT C.cname
FROM   Customers C LEFT JOIN Likes L
    ON C.cname = L.cname
WHERE  L.pizza IS NULL; -- keep only dangling tuples

-- Can also use EXCEPT command
SELECT cname FROM Customers
EXCEPT
SELECT DISTINCT cname FROM Likes
```


```sql
SELECT *
FROM student s, department d 
WHERE s.department = d.department
```


```sql
SELECT *
FROM student s LEFT OUTER JOIN department d 
	ON s.department = d.department
```