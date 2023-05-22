
##### IN vs = ANY

```sql
WHERE <expr> IN <subquery> 
```

is equivalent to 

```sql
WHERE <expr> = ANY <subquery>
```

##### ANY vs EXISTS

```sql
:
WHERE <e1> <op> ANY (
	SELECT <e2>
	FROM <rel>
	WHERE <cond>
);
```

is equivalent to 

```sql
:
WHERE EXISTS (
	SELECT *
	FROM <rel>
	WHERE <cond> 
	AND <e1> <op> <e2> -- bring comparison op inside
);
```