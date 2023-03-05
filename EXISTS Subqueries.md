
```sql
:
WHERE [ NOT ] EXISTS <subquery>;
```

Note:
- The subquery may return **any number of columns**
- `EXISTS` returns `TRUE` if the subquery returns _at least one_ row
- `NOT EXISTS` returns `TRUE` if the subquery returns _no_ row

Example:

```sql
-- Find all areas for which Diavola is sold by at least one restaurant.

SELECT DISTINCT area
FROM   Restaurants R
WHERE EXISTS (SELECT 1 -- any number works
		    FROM   Sells S
		    WHERE  S.rname = R.rname
		    AND  S.pizza = 'Diavola');
```

```sql
-- Find all customer names and areas for which there is no restaurant in the area.

SELECT *
FROM   Customers C
WHERE NOT EXISTS (SELECT 1
		        FROM   Restaurants R
	            WHERE  C.area = R.area);
```


>[!tip]
> This command is useful when query asks for existence through keywords **"at least"** or **"no"**
