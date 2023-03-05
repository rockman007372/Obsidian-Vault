
## Motivation: Circular Reference

```sql
CREATE TABLE Employee (
  eid   INT PRIMARY KEY,
  name  TEXT,
  did   INT
);

```

```sql
CREATE TABLE Department (
  did   INT PRIMARY KEY,
  name  TEXT,
  eid   INT
);
```

> An employee must work in a department.

```sql
ALTER TABLE Employee ADD CONSTRAINT
  did_fk FOREIGN KEY (did)
  REFERENCES Department (did);

```

> A department must be managed by an employee.

```sql
ALTER TABLE Department ADD CONSTRAINT
  eid_fk FOREIGN KEY (eid)
  REFERENCES Employee (eid);
```

## Not Deferrable

Default behaviour is to check constraints at every insertion.

```sql
BEGIN;  -- start of transaction

INSERT INTO Employee VALUES (101, 'Sarah', 1001); -- Violation → abort
INSERT INTO Department VALUES (1001, 'dev', 101); -- Not executed

COMMIT; -- successful end of transaction
```

```sql
ALTER TABLE Employee ADD CONSTRAINT
  did_fk FOREIGN KEY (did)
  REFERENCES Department (did)
  NOT DEFERRABLE; -- Standard behaviour

ALTER TABLE Department ADD CONSTRAINT
  eid_fk FOREIGN KEY (eid)
  REFERENCES Employee (eid)
  NOT DEFERRABLE;
```

## Initially Deferred

Defer the constraint checks until the first commit.

```sql
BEGIN;  -- start of transaction

INSERT INTO Employee VALUES (101, 'Sarah', 1001); -- deferred
INSERT INTO Department VALUES (1001, 'dev', 101); -- deferred

COMMIT; -- Check all constraints, successful end of transaction
```

```sql
ALTER TABLE Employee ADD CONSTRAINT
  did_fk FOREIGN KEY (did)
  REFERENCES Department (did)
  DEFERRABLE INITIALLY DEFERRED;

ALTER TABLE Department ADD CONSTRAINT
  eid_fk FOREIGN KEY (eid)
  REFERENCES Employee (eid)
  DEFERRABLE INITIALLY DEFERRED;
```

## Initially Immediate

Only defer one particular transaction (row(s) insertion). The subsequent transactions is back to immediate.

```sql
BEGIN;  -- start of transaction

SET CONSTRAINTS did_fk DEFERRED;
INSERT INTO Employee VALUES (101, 'Sarah', 1001); -- Deferred
INSERT INTO Department VALUES (1001, 'dev', 101); -- Check constraints, success

COMMIT; -- successful end of transaction
```

```sql
ALTER TABLE Employee ADD CONSTRAINT
  did_fk FOREIGN KEY (did)
  REFERENCES Department (did)
  DEFERRABLE INITIALLY IMMEDIATE;
```