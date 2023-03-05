
>[!definition]
> A primary key is a selected candidate key.
> - Uniquely identifies a tuple in a relation.
> - Primary key attributes cannot be NULL.

In other word, it requires both [[Unique Constraint]] and [[Not-NULL Constraint]]

## Column

```sql
CREATE TABLE Employees (
  id    INT  PRIMARY KEY,
  name  TEXT,
  age   INT,
  role  TEXT
);
```

```sql
CREATE TABLE Employees (
  id    INT  CONSTRAINT emp_pk PRIMARY KEY,
  name  TEXT,
  age   INT,
  role  TEXT
);
```

## Table

```sql
CREATE TABLE Teams (
  eid   INT,
  pname TEXT,
  hours INT,
  PRIMARY KEY (eid, pname)
);
```

```sql
CREATE TABLE Teams (
  eid   INT,
  pname TEXT,
  hours INT,
  CONSTRAINT team_pk PRIMARY KEY (eid, pname)
);
```

This is equivalent to:

```sql
CREATE TABLE Teams (
  eid   INT  NOT NULL,
  pname TEXT NOT NULL,
  hours INT,
  UNIQUE (eid, pname)
);
```

