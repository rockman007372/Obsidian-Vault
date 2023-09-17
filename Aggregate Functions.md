Aggregate functions in SQL compute **a single value** from a set of tuples.

>[!Example]
> Find the lowest and highest price pizza among all the restaurants that sells at least one pizza.
 
```SQL
SELECT MIN(price) AS lowest,
       MAX(price) AS highest
FROM   Sells;
```

## Common aggregation functions and interpretations

Usually, aggregate functions do not count NULL values.

```sql
SELECT MIN(A) FROM R;   -- Minimum non-NULL values in column A
SELECT MAX(A) FROM R;   -- Maximum non-NULL values in column A
SELECT AVG(A) FROM R;   -- Average of non-NULL values in column A
SELECT SUM(A) FROM R;   -- Sum of non-NULL values in column A
SELECT COUNT(A) FROM R; -- Count of non-NULL values in column A
SELECT COUNT(*) FROM R; -- Count of ALL rows in column A
```

You can apply functions over **distinct values**. Take note that `IS DISTINCT` operation is used to check (Eg. `NULL IS DISTINCT FROM NULL == FALSE`)

```sql
SELECT AVG(DISTINCT A) FROM R;
SELECT SUM(DISTINCT A) FROM R;
SELECT COUNT(DISTINCT A) FROM R;
```

### Edge cases

Let R be an *empty relation* with attribute A.

```sql
SELECT MIN(A) FROM R; -- NULL
SELECT MAX(A) FROM R; -- NULL
SELECT AVG(A) FROM R; -- NULL
SELECT SUM(A) FROM R; -- NULL

SELECT COUNT(A) FROM R -- 0
SELECT COUNT(*) FROM R -- 0
```

Let S be a *non-empty relation* with n-rows and with *attribute A that only has NULL values*.

```sql
SELECT MIN(A) FROM R; -- NULL
SELECT MAX(A) FROM R; -- NULL
SELECT AVG(A) FROM R; -- NULL
SELECT SUM(A) FROM R; -- NULL

SELECT COUNT(A) FROM R -- 0
SELECT COUNT(*) FROM R -- n
```