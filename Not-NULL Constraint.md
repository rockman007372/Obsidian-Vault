
## Column constraint

```sql
CREATE TABLE Employees ( 
	id INT NOT NULL, 
	name TEXT NOT NULL, 
	age INT, 
	role TEXT 
);
```

```sql
CREATE TABLE Employees ( 
	id INT CONSTRAINT nn_id NOT NULL, 
	name TEXT CONSTRAINT nn_name NOT NULL, 
	age INT,
	role TEXT 
);
```