A **stored function** is a user-defined function that is stored in a database and can be called from within SQL queries.

# Return values

SQL functions either return:
- A single return value of a specific type
- An **existing** tuple (row) or set of tuples (table)
- A **new** tuple or new set of tuples
## Single Value

```sql
CREATE OR REPLACE FUNCTION convert(mark INT)
RETURNS char(1) AS $$
  SELECT   CASE
  WHEN mark >=70 THEN 'A'
  WHEN mark >= 60 THEN 'B'
  WHEN mark >= 50 THEN 'C'
  ELSE    'D'
  END;
$$ LANGUAGE sql;
```

We can combine this function into our query as if it is an [[Aggregate Functions]]:

```sql
SELECT Name, convert(Mark) 
FROM Scores;
```

```sql
SELECT Name  
FROM   Scores  
WHERE convert(Mark) = 'B';
```

We can rewrite the function above with `IN` and `OUT` mode of argument:

```sql
CREATE OR REPLACE FUNCTION convert
	(IN mark INT, OUT grade CHAR(1))
AS $$
BEGIN
	IF mark >= 70 THEN
		grade := 'A'
	ELSE IF...
	END IF;
END;
$$ LANGUAGE plpgsql;
```

Note that this function does not return any value explicitly. We can retrieve the returned value by `select grade from convert(...)`:

```sql
SELECT Name, (SELECT grade FROM convert(Mark)) AS Grade
FROM Scores;
```

## Existing Tuples

### One tuple
- Note that you must return all the columns in table Scores, else exception.
```sql
CREATE OR REPLACE FUNCTION topStudent()
RETURNS Scores AS $$
  SELECT *
  FROM Scores
  ORDER BY Mark DESC 
  LIMIT 1;
$$ LANGUAGE sql;
```

### Multiple tuples

```sql
CREATE OR REPLACE FUNCTION topStudents()
RETURNS SETOF Scores AS $$
  SELECT *
  FROM Scores
  WHERE Mark = (SELECT MAX(Mark) FROM Scores);
$$ LANGUAGE sql;
```

## New Tuples
### Multiple tuples

>[!question]
> Find all the marks and their number of occurences.

Method 1:

```sql
CREATE OR REPLACE FUNCTION markCount()
RETURNS TABLE(Mark INT, Cnt INT) AS $$
  SELECT     Mark, COUNT(*)
  FROM       Scores
  GROUP BY   Mark ;
$$ LANGUAGE sql;
```

Method 2:

```sql
CREATE OR REPLACE FUNCTION markCount
	(OUT Mark INT, OUT Cnt INT)
RETURNS SETOF RECORD AS $$
  SELECT Mark, COUNT(*)
  FROM   Scores
  GROUP BY   Mark ;
$$ LANGUAGE sql;
```

Difference between the above queries:
- `SETOF RECORD` requires at least 2 columns to be returned while `TABLE` does not.


# Assignment

1. Basic assignment

```sql
mark := 100
```

2. `SELECT... INTO ...`

```SQL
DECLARE
	mark INTEGER;
BEGIN
	SELECT s.points INTO mark 
	FROM student s
	WHERE id = 1;
END;
```

```SQL
DECLARE
	maxScore INT;
	minScore INT;
BEGIN
	SELECT MAX(score), MIN(score) INTO maxScore, minScore
	FROM student s;
END;
```

