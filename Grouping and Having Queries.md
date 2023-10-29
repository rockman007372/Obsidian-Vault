
## GROUP BY

```sql
GROUP BY attr1, attr2,...
```

- Logical partition of relation into groups based on values for specified attributes. (In reality, no actual reordering performed)
- ! In principle, always applied together with [[Aggregate Functions]]
- @ Application of aggregation function are now **over each group** (one result tuple for each group)

> [!Example]
> For each restaurant, find the lowest and highest price pizza

```sql
SELECT rname, MIN(price), MAX(price)
FROM   Sells
GROUP BY rname;
```

##### Restrictions of `GROUP BY` on `SELECT` clause:

If column $A_i$ of table R appears in the `SELECT` clause, one of the following conditions must hold:
1. $A_i$ appears in the `GROUP BY` clause
2. $A_i$ appears as an **input of an aggregation function** in the `SELECT` clause
3. The primary key of R appears in the `GROUP BY` clause. **(not candidate key)**

Reason: to avoid ambiguity about which $A_i$ of which row to select.

```sql
-- Valid
SELECT rname, SUM(price)
FROM   Sells
GROUP BY rname;

-- Valid
SELECT rname, pizza, price -- price is not ambiguous
FROM   Sells
GROUP BY rname, pizza; -- {rname, pizza} is PK of Sells

-- Invalid
SELECT rname, pizza, SUM(price) -- pizza is ambiguous
FROM   Sells
GROUP BY rname; -- rname is not PK of Sells
```


## HAVING

```sql
GROUP BY attr1, attr2, ...
HAVING <condition>
```

**Notes:**
- Condition check for each group defined in `GROUP BY`
- ! Cannot be used without `GROUP BY` clause
- Conditions typically (but not always) involve aggregate functions

>[!example]
> Find all restaurants and the number of pizza they sells such that the restaurant sells more than 1 pizza.

```sql
SELECT rname, COUNT(pizza)
FROM   Sells
GROUP BY rname
HAVING COUNT(pizza) > 1;
```

**Restrictions:**

If column _Ai_ of table _R_ appears in the `HAVING` clause, one of the following conditions must hold

1.  _Ai_ appears in the `GROUP BY` clause
2.  _Ai_ appears as input of an aggregation function in the `HAVING` clause
3.  The primary key ~~or a candidate key~~ of _R_ appears in the `GROUP BY` clause

```sql
-- Valid
SELECT rname, COUNT(*) 
FROM Sells
GROUP BY rname 
HAVING AVG(price) > 20; -- Aggregate function

-- Valid
SELECT rname, COUNT(*) 
FROM Sells
GROUP BY rname, pizza -- (rname, pizza) is PK of Sells
HAVING price > 20;

-- Invalid
SELECT rname, COUNT(*) FROM Sells
GROUP BY rname HAVING price > 20;
```



## Exercises

>[!question]
> Find all the restaurants that sells any pizza cheaper than any pizza sold by Lorenzo Tavern

```sql
SELECT rname
FROM Sells
GROUP BY rname
HAVING MIN(price) < 
	(SELECT MAX(price) FROM Sells WHERE rname = 'Lorenzo')
```