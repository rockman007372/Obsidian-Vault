
These following SQL functions either return:
- A single return value of a specific type
- An **existing** tuple (row) or set of tuples (table)
- A **new** tuple or new set of tuples

### Single Value

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

### Existing Tuples

One tuple:

```sql
CREATE OR REPLACE FUNCTION topStudent()
RETURNS Scores AS $$
  SELECT *
  FROM Scores
  ORDER BY Mark DESC 
  LIMIT 1;
$$ LANGUAGE sql;
```

Multiple tuples:

```sql
CREATE OR REPLACE FUNCTION topStudents()
RETURNS SETOF Scores AS $$
  SELECT *
  FROM Scores
  WHERE Mark = (SELECT MAX(Mark) FROM Scores);
$$ LANGUAGE sql;
```

### New Tuples

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
CREATE OR REPLACE FUNCTION markCount(OUT Mark INT, OUT Cnt INT)
RETURNS SETOF RECORD AS $$
  SELECT Mark, COUNT(*)
  FROM   Scores
  GROUP BY   Mark ;
$$ LANGUAGE sql;
```