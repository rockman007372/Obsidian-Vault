### Before

`BEFORE`: If value returned is `null`, no operation will be done. Else, operation happens as per normal.

```sql
CREATE OR REPLACE FUNCTION scores_log_func() RETURNS TRIGGER AS $$

BEGIN
	INSERT INTO Scores_Log(Name, EntryDate); 
    VALUES (NEW.Name, CURRENT_DATE);
	RETURN NULL; -- No operation is done
END;

$$ LANGUAGE plpgsql;
```

```sql
CREATE TRIGGER scores_log_trigger
BEFORE INSERT ON Scores
FOR EACH ROW EXECUTE FUNCTION scores_log_func();
```

### After

`AFTER`: The return value **does not matter.** The trigger function is invoked after the main operation is done.

```sql
CREATE TRIGGER scores_log_trigger
AFTER INSERT ON Scores -- operation is already done
FOR EACH ROW EXECUTE FUNCTION scores_log_func();
```