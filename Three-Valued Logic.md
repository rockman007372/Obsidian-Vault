
Consist of True, False, NULL.

## Logic Table

![[Pasted image 20230123151253.png]]


![[Pasted image 20230123151305.png]]

## Relational & Arithmetic Operations 

- Any relational/arithmetic operation with NULL produces NULL values:

```sql
NULL < 2023
NULL >= 0
id = NULL
id <> NULL
-- these all produce NULL values
```

- We add operators to treat NULL as values: `IS DISTINCT FROM`

![[Pasted image 20230124154817.png]]

Example:

```sql
SELECT *
FROM my_table
WHERE column1 IS DISTINCT FROM column2;
```