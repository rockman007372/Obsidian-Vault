
In some scenarios, we have to deferred the checking of triggers because intermediate states of the transation may activate trigger. 

Assume the trigger throws exception if the total balance is less than 150 at any time. The following transaction will violate the constraint:

```sql
BEGIN TRANSACTION;
	UPDATE Account SET Bal = Bal – 100 WHERE AID = 1; -- violate
	UPDATE Account SET Bal = Bal + 100 WHERE AID = 2;
	COMMIT;
END TRANSACTION;
```

Hence, we must defer the trigger until the end of the transation!

### DEFERRABLE INITIALLY DEFERRED

We can defer the trigger check until **the end of the transation** using `DEFERRABLE INITIALLY DEFERRED` in the trigger.

```sql
CREATE CONSTRAINT TRIGGER bal_check_trigger -- MUST ADD CONSTRAINT
AFTER INSERT OR UPDATE OR DELETE ON Account
DEFERABLE INITIALLY DEFERRED -- DEFINE CONSTRAINT
FOR EACH ROW
EXECUTE FUNCTION bal_check_func();
```

Note:
- ! `CONSTRAINT` must be specified for deferred triggers

### DEFERRABLE INITIALLY IMMEDIATE

We can also set `DEFERABLE INITIALLY IMMEDIATE` to the **trigger** and defer the constraint on the go in the **transaction**:

```sql
-- TRIGGER
CREATE CONSTRAINT TRIGGER bal_check_trigger
AFTER INSERT OR UPDATE OR DELETE ON Account
DEFERABLE INITIALLY IMMEDIATE
FOR EACH ROW
EXECUTE FUNCTION bal_check_func();

-- TRANSACTION
BEGIN TRANSACTION;
	SET CONSTRAINTS bal_check_trigger DEFERRED; -- stated on the go
	UPDATE Account SET Bal = Bal – 100 WHERE AID = 1;
	UPDATE Account SET Bal = Bal + 100 WHERE AID = 2;
	COMMIT; -- constraint checked here
END TRANSATION;
```

---
Links: [[PL-pgSQL|PL/pgSQL]], [[Deferrable Constraints]]