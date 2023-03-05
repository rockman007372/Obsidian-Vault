## CHECK Constraint

- Most basic general constraint (i.e., not a structural integrity constraint)
- Allows us to specify that column values must satisfy _an arbitrary Boolean expression_
- ! **Scope:** _ONE table or ONE row_

##### One Row

```sql
CREATE TABLE Projects (
  eid    INT,
  pname  TEXT,
  hours  INT CHECK (hours > 0),
  PRIMARY KEY (eid, pname)
);
```

##### One Table

```sql
CREATE TABLE Teams (
  name        TEXT PRIMARY KEY,
  start_year  INT,
  end_year    INT,
  CHECK (start_year <= end_year)
);
```

##### If Else Statement

>[!example]
>Create the Table "Teams" where the minimum hours for 'CoreOS' is at least 30 hours but there are no such restrictions for other projects.

We make use of if else logic and its equivalence: `p → q === ~p v q`

```sql
CREATE TABLE Projects (
  eid    INT,
  pname  TEXT,
  hours  INT CHECK (hours > 0),
  PRIMARY KEY (eid, pname),
  CHECK (
    (pname <> 'CoreOS' OR hours >= 30)
  )
);
```