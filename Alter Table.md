## Alter Table

##### Syntax

```sql
ALTER TABLE <table_name>
	[ALTER / ADD / DROP] [COLUMN / CONSTRAINT] <name>
	<changes>;
```

Common modifications:
- Adding / dropping columns
- Adding / dropping constraints
- Changing the specification (data type/ default values...) of a single column.

##### Adding / Dropping Columns

```sql
ALTER TABLE Projects 
	ADD COLUMN budget 
	NUMERIC DEFAULT 0.0;

ALTER TABLE Projects 
	DROP COLUMN budget;
```

##### Adding / Dropping Constraints

```sql
ALTER TABLE Teams 
	ADD CONSTRAINT
	eid_fkey FOREIGN KEY (eid) REFERENCES Employees (id);

ALTER TABLE Teams 
	DROP CONSTRAINT eid_fkey;
```

>[!attention]
> Name of constraints need to be **known** (may be retrieved from metadata)

##### Changing Specification of a Single Column

```sql
ALTER TABLE Projects 
	ALTER COLUMN name 
	TYPE VARCHAR(200);
```

```sql
ALTER TABLE Projects 
	ALTER COLUMN start_year 
	SET DEFAULT 2021;
```

```sql
ALTER TABLE Projects 
	ALTER COLUMN name 
	DROP DEFAULT;

```