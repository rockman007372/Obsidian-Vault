
>[!example]
> Find all customers in Central area that like at least one pizza sold by Corleone Corner (exclude customers that do not like any pizza).

```sql
-- Customers in Central
SELECT C.cname
FROM   Customers C
WHERE  C.area = 'Central'
AND  C.cname IN 

	-- ALL customers who like at least one pizza
	(SELECT L.cname
	 FROM   Likes L
	 WHERE  L.pizza IN

		-- Sold by Corleone Corner
		(SELECT S.pizza
		 FROM   Sells S
		 WHERE  S.rname = 'Corleone Corner')
);
```

This is equivalent to a joined query:

```sql
SELECT DISTINCT C.cname -- must be DISTINCT to remove duplicate
FROM Customers C, Likes L, Sells S 
WHERE C.area = 'Central'
AND C.cname = L.cname
AND S.pizza = L.pizza
AND S.rname = 'Corleone Corner';
```

and 

```sql
SELECT c.cname
FROM Customers c
WHERE c.area = 'Central'
AND EXISTS (
	SELECT 1 
	FROM Likes l
	WHERE l.cname = c.cname -- important
	AND l.pizza IN (select pizza from Sells where rname = 'Corleone Corner')
)
```