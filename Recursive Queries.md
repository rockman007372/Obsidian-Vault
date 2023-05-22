## Motivation

```sql
CREATE TABLE MRT ( 
	fr_stn CHAR(5), 
	to_stn CHAR(5), 
	PRIMARY KEY (fr_stn, to_stn) 
);
```

> [!question]
> Find all MRT station that can be reached from NS1 in n-stops

## Form

```sql
WITH RECURSIVE 
	CTE_name AS ( 
		Q_1 
		UNION [ ALL ] 
		Q_2 ( CTE_name ) 
	) 
Q_0 ( CTE_name )
```

- Q_1 is non-recursive (**base query**). 
- Q_2 is recursive and can reference CTE_name. 
- Query is evaluated "lazily", stops when a fixed-point is reached.

## Solution

Find all MRT station that can be reached from NS1 in **at most** 3-stops

```sql
WITH RECURSIVE
	Linker(to_stn, stops) AS (
		SELECT to_stn, 0
		FROM MRT
		WHERE fr_stn = 'NS1'
		
		UNION ALL
		
		SELECT M.to_stn, L.stops + 1
		FROM Linker L, MRT M
		WHERE L.to_stn = M.fr_stn
		AND L.stops < 2 -- stopping condition
	)

SELECT DISTINCT(to_stn)
FROM Linker
```

You can bring the condition down into Q_0.

```sql
WITH RECURSIVE
	Linker(to_stn, stops) AS (
		SELECT to_stn, 0
		FROM MRT
		WHERE fr_stn = 'NS1'
		
		UNION ALL
		
		SELECT M.to_stn, L.stops + 1
		FROM Linker L, MRT M
		WHERE L.to_stn = M.fr_stn
	)

SELECT DISTINCT(to_stn)
FROM Linker L
WHERE L.stopS <= 3
```

