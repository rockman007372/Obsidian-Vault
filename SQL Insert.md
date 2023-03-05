## SQL Insert

```SQL
INSERT INTO Employees 
	VALUES (101, 'Sarah', 25, 'dev');
```

![[Pasted image 20230201170343.png]]

```SQL
INSERT INTO Employees (name, id) 
	VALUES 
		('Judy', 102), 
		('Max', 103);
```

![[Pasted image 20230201170444.png]]

>[!Note]
> - Either all inserted or none inserted (if constraint is violated)
> - Attributes can be specified out of order
> - Missing values are replaced with either NULL or DEFAULT VAL