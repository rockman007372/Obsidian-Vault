
## Column Constaint

```SQL
CREATE TABLE Employees ( 
	id INT UNIQUE, 
	name TEXT, 
	age INT, 
	role TEXT );
```

```SQL
CREATE TABLE Employees ( 
	id INT CONSTRAINT emp_id UNIQUE, 
	name TEXT , 
	age INT, 
	role TEXT 
);
```

## Table Constraint

```sql
CREATE TABLE Teams ( 
	eid INT, 
	pname TEXT, 
	hours INT, 
	UNIQUE (eid, pname) 
);
```

```sql
CREATE TABLE Teams ( 
	eid INT, 
	pname TEXT, 
	hours INT, 
	CONSTRAINT team_id UNIQUE (eid, pname) 
);
```

