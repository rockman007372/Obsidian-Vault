
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
  did_fk FOREIGN KEY (did) REFERENCES Department (did);

```

> A department must be managed by an employee.

```sql
ALTER TABLE Department ADD CONSTRAINT
  eid_fk FOREIGN KEY (eid) REFERENCES Employee (eid);
```

These 2 foreign key constraints prevent any tuple from being inserted into either table!

## Not Deferrable

Default behaviour is `NOT DEFERREABLE`.  This means constraints are checked after each **update on individual row**. 

>[!note]
> Notice that constraint is checked at row level, not statement level!

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

```sql
BEGIN;  -- start of transaction

INSERT INTO Employee VALUES (101, 'Sarah', 1001); -- Violation → abort
INSERT INTO Department VALUES (1001, 'dev', 101); -- Not executed

COMMIT; -- successful end of transaction
```

## Initially Deferred

We can defer the constraint checks until the **first commit of the transaction** using `DEFERRABLE INITIALLY DEFERRED`.

```sql
ALTER TABLE Employee 
	ADD CONSTRAINT
	  did_fk FOREIGN KEY (did) REFERENCES Department (did)
	  DEFERRABLE INITIALLY DEFERRED;

ALTER TABLE Department 
	ADD CONSTRAINT
	  eid_fk FOREIGN KEY (eid) REFERENCES Employee (eid)
	  DEFERRABLE INITIALLY DEFERRED;
```

```sql
BEGIN;  -- start of transaction

INSERT INTO Employee VALUES (101, 'Sarah', 1001); -- deferred
INSERT INTO Department VALUES (1001, 'dev', 101); -- deferred

COMMIT; -- Check all constraints, successful end of transaction
```

## Initially Immediate

With `DEFERRABLE INITIALLY IMMEDIATE`, the constraint will STILL be checked **after each statement** in the transaction. However, you have the option to set the constraint to `DEFERRABLE INITIALLY DEFERRED` using the command `SET CONSTRAINT __ DEFERRED`.

If you execute the `SET CONSTRAINTS` command with the `DEFERRED` option within a transaction, it will change the behavior of the specified constraint from `IMMEDIATE` to `DEFERRED` for the duration of that transaction. This means that the constraint will not be checked immediately after each statement, but rather at the end of the transaction when you issue the `COMMIT` command .

```sql
ALTER TABLE Employee ADD CONSTRAINT
  did_fk FOREIGN KEY (did)
  REFERENCES Department (did)
  DEFERRABLE INITIALLY IMMEDIATE;
```

```sql
BEGIN;  -- start of transaction

SET CONSTRAINTS did_fk DEFERRED;
INSERT INTO Employee VALUES (101, 'Sarah', 1001); -- Deferred
INSERT INTO Department VALUES (1001, 'dev', 101); -- Check constraints, success

COMMIT; -- successful end of transaction
```

More info: [sql - NOT DEFERRABLE versus DEFERRABLE INITIALLY IMMEDIATE - Stack Overflow](https://stackoverflow.com/questions/5300307/not-deferrable-versus-deferrable-initially-immediate)
