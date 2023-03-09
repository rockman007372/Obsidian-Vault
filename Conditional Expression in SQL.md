## CASE expression

```sql
CASE
	WHEN <condition_1> THEN <result_1>
	WHEN <condition_2> THEN <result_2>
	⁝
	WHEN <condition_n> THEN <result_n>
	ELSE result_0
END

CASE <expression>
	WHEN <value_1> THEN <result_1>
	WHEN <value_2> THEN <result_2>
	⁝
	WHEN <value_n> THEN <result_n>
	ELSE <result_0>
END
```

Examples:

![[Pasted image 20230307134645.png||300]]

```sql
SELECT rname, CASE
    WHEN AVG(price) >= 23 THEN 'Expensive'
    WHEN AVG(price) >= 18 THEN 'Reasonable'
    ELSE 'Cheap'
  END
FROM Sells
GROUP BY rname;
```

## COALESCE expression

```sql
COALESCE(<value_1>, <value_2>, <value_3>, ...)
```

- Return the **first** non-NULL values in the list of input argument.
- Returns NULL if all the arguments are NULL

Equivalent to:

```sql
CASE
	WHEN <value_1> IS NOT NULL THEN <value_1>
	WHEN <value_2> IS NOT NULL THEN <value_2>
	ELSE <value_3>
END
```

## NULLIF expression

```sql
NULLIF(<value_1>, <value_2>)
```

Returns `NULL` if `<value_1> = <value_2>`, otherwise returns `<value_1>`

Usage:

> [!example]
> Find the minimum and average price of pizza across different restaurants. However, since _unknown_ values are represented as 0 (instead of `NULL`), _exclude the unknown values from the computation_.

```sql
SELECT MIN(NULLIF(price,0)) AS min_price,
	   AVG(NULLIF(price,0)) AS avg_price
FROM   Sells;
```