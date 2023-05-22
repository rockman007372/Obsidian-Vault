
>[!example]
> Find all customers in Central area that like at least one pizza sold by Corleone Corner (exclude customers that do not like any pizza).

```sql
-- Customers in Central
SELECT C.cname
FROM   Customers C
WHERE  area = 'Central'
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

This is equivalent to:

```sql
SELECT DISTINCT c.cname -- must be DISTINCT to remove duplicate
FROM Customers C, Likes L, Sells S 
WHERE C.area = 'Central'
AND C.cname = L.cname
AND S.pizza = L.pizza
AND S.rname = 'Corleone Corner';
```