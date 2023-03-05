## SQL Delete

```sql
DELETE FROM <table_name>
	[ WHERE <condition> ] -- optional
```

Condition is optional:
- If unspecified, always true
- ? if specified, condition can be arbitrary complex

>[!Principle of Acceptance]
>Perform the operation only if the condition evaluates to **True** (not NULL)

```SQL
DELETE FROM EMPLOYEES; -- delete all rows
```

```SQL
DELETE FROM Employees
	WHERE role <> 'dev';
```

![[Pasted image 20230201171323.png]]

`NULL <> 'dev' == NULL`, hence last row is not deleted.