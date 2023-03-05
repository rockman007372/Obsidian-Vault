
**Foreign key constraints** are the rules created when we add a [[Foreign Key]] to a table. 

>[!Important]
> Each foreign key in R1 must satisfy one of the following:
> - Appear as **primary key** in R2 (meaning it must **exist** in R2) or
> - Be a NULL value (or a tuple containing at least one NULL value)

## Example

**Referencing Relation:**

```sql
CREATE TABLE Teams (
  eid     INT,
  pname   TEXT REFERENCES Projects,
  hours   INT,
  PRIMARY KEY (eid, pname),
  FOREIGN KEY (eid) REFERENCES Employees (id)
);
```

**Referenced Relations:**

```sql
CREATE TABLE Employees (
  id    INT  PRIMARY KEY,
  name  TEXT,
  age   INT,
  role  TEXT
);
```

```sql
CREATE TABLE Projects (
  name        TEXT,
  start_year  INT,
  end_year    INT,
  PRIMARY KEY (name)
);
```

Note:
- Since each relation can only have one primary key, you can just reference the relation without specifying the primary key!
	- In reality, a foreign key can reference any candidate key and not just primary key. Hence it's good practice to specify which attributes are being referenced.
- As long as there is at least one NULL value, foreign key constraint is satisfied.

## Delete/Update Behaviour

Extend the syntax to specify the _behavior_ when data in referenced table is deleted or updated using _optional_ specification:

-   `ON DELETE <action>`
-   `ON UPDATE <action>`

![[Pasted image 20230204231806.png]]

```sql
CREATE TABLE Teams (
  eid    INT,
  pname  TEXT DEFAULT 'FastCash',
  hours  INT,
  PRIMARY KEY (eid, pname),
  FOREIGN KEY (eid) REFERENCES Employees (id) 
	  ON DELETE NO ACTION ON UPDATE CASCADE,
  FOREIGN KEY (pname) REFERENCES Projects (name) 
	  ON DELETE SET DEFAULT ON UPDATE CASCADE
);
```

##### Effects
-   Updates on _Employees.id_ and _Projects.name_ are _propagated_
-   Deleting a project will set _Teams.pname_ to _default value_ (i.e., FastCash)
-   Deleting an employee will _raise an error_ if that employee is still assigned to a team

#### Practical Considerations
-   Specified constraints might not behave as expected
    -   `SET NULL` issue with prime attributes (attributes of primary key)
    -   `SET DEFAULT` issue with default value not in referenced relation
    -   `CASCADE` may create a _chain_ of propagation (if the referencing relation is also a referenced relation)
-   `CASCADE` may _significantly_ affect overall performance