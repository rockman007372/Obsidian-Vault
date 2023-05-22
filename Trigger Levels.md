## Trigger Levels

- `FOR EACH ROW`: **row-level** trigger that executes the trigger function for every row / tuple encountered.

- `FOR EACH STATEMENT`: **statement-level** trigger, activate once for every statement / operation.

**Example:** 
If we declare `FOR EACH ROW`, the same notice will show up repeatedly if there we insert mutiple rows. Therefore, we use `FOR EACH STATEMENT` to limit notice to one per statement.

```sql
CREATE OR REPLACE FUNCTION del_warn_func() RETURNS TRIGGER AS $$
BEGIN
        RAISE NOTICE 'You are not supposed to delete from the log.';
        RETURN NULL; -- DOES NOT PREVENT DELETION?
END;
$$ LANGUAGE plpgsql;
```

```sql
CREATE TRIGGER del_warn_trigger
BEFORE DELETE ON Scores_Log
FOR EACH STATEMENT EXECUTE FUNCTION del_warn_func();
```

Note that statement-level triggers **ignore returned values**! This means returning `null` will not stop the operations from being executed.

How to prevent subsequent operations in statement-level triggers? → **Raise exceptions**.

```sql
CREATE OR REPLACE FUNCTION del_warn_func() RETURNS TRIGGER AS $$
BEGIN
        RAISE EXCEPTION 'No deletion from the log is allowed.';
        RETURN NULL;
END;
$$ LANGUAGE plpgsql;
```

>[!Trigger Timing vs Levels]
> - INSTEAD OF is **only allowed on row-level**
> - BEFORE/AFTER are allowed on both levels