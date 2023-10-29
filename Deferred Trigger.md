
In some scenarios, we have to deferred the checking of triggers because intermediate states of the transation may activate trigger. 

Assume the trigger throws exception if the total balance is less than 150 at any time. 

```SQL
CREATE TRIGGER bal_check_trigger
BEFORE UPDATE ON Account
FOR EACH ROW
EXECUTE FUNCTION bal_check_func(); -- throw exception if total < 150
```

The following transaction will violate the constraint:

```sql
BEGIN TRANSACTION;
	UPDATE Account SET Bal = Bal – 100 WHERE AID = 1; -- violate
	UPDATE Account SET Bal = Bal + 100 WHERE AID = 2;
	COMMIT;
END TRANSACTION;
```

Hence, we must defer the trigger until the end of the transation!

### DEFERRABLE INITIALLY DEFERRED

`DEFERRABLE INITIALLY DEFERRED` allows us to defer the trigger check until **the end of the transation** (when you call `COMMIT`).

```sql
CREATE CONSTRAINT TRIGGER bal_check_trigger -- MUST ADD CONSTRAINT
AFTER INSERT OR UPDATE OR DELETE ON Account -- MUST BE AFTER
DEFERRABLE INITIALLY DEFERRED -- DEFINE CONSTRAINT
FOR EACH ROW
EXECUTE FUNCTION bal_check_func();
```

Note:
- ! `CONSTRAINT` must be specified for deferred triggers
- A constraint trigger can only be specified as `AFTER`.
	- By default, all `BEFORE` triggers are fired first.

### DEFERRABLE INITIALLY IMMEDIATE

`DEFERABLE INITIALLY IMMEDIATE` allows us to toggle the deferrable constraint on the go in the **transaction**.

```sql
-- TRIGGER
CREATE CONSTRAINT TRIGGER bal_check_trigger
AFTER INSERT OR UPDATE OR DELETE ON Account
DEFERRABLE INITIALLY IMMEDIATE -- toggle deferrable on the go
FOR EACH ROW
EXECUTE FUNCTION bal_check_func();

-- TRANSACTION
BEGIN TRANSACTION;
	-- toggle constraint
	SET CONSTRAINTS bal_check_trigger DEFERRED; 
	
	UPDATE Account SET Bal = Bal – 100 WHERE AID = 1;
	UPDATE Account SET Bal = Bal + 100 WHERE AID = 2;
	COMMIT; -- constraint checked here
END TRANSATION;
```

---
Links: [[PL-pgSQL|PL/pgSQL]], [[Deferrable Constraints]]