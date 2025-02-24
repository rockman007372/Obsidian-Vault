### Example 1

Whenever there is a new tuple inserted into Scores, we insert a value into `Scores_Log` to record:
- name of student
- date of insertion

```sql
CREATE OR REPLACE FUNCTION scores_log_func() RETURNS TRIGGER AS $$

BEGIN
  INSERT INTO Scores_Log(Name, EntryDate)
  VALUES (NEW.Name, CURRENT_DATE);
  
  RETURN NULL;
END;

$$ LANGUAGE plpgsql;
```

```sql
CREATE TRIGGER scores_log_trigger
AFTER INSERT ON Scores
FOR EACH ROW 
EXECUTE FUNCTION scores_log_func();
```

Note:
- Trigger function must `RETURN TRIGGER` to access the new tuple through keyword `NEW`
- Trigger functions can also access these fields:
	- `TG_OP`: Operations that activate the triggers
	- `TG_TABLE_NAME`: Name of table that caused the trigger 
	- `OLD`: the old tuple being updated / deleted

### Example 2

For each operations on `Scores` table, we want to record:

- name of student
- type of operation
- date of operation

into the table `Record_Logs`.

```sql
CREATE OR REPLACE FUNCTION scores_log2_func() RETURNS TRIGGER AS $$

BEGIN
        IF (TG_OP = 'INSERT') THEN
                INSERT INTO Scores_Log2 
	                SELECT NEW.Name, 'Insert', CURRENT_DATE;
                RETURN NEW; -- no need since AFTER keyword
                
        ELSEIF (TG_OP = 'UPDATE') THEN
                INSERT INTO Scores_Log2 
	                SELECT NEW.Name, 'Update', CURRENT_DATE;
                RETURN NEW; -- no need since AFTER keyword
                
        ELSEIF (TG_OP = 'DELETE') THEN
                INSERT INTO Scores_Log2 
	                SELECT OLD.Name, 'Delete', CURRENT_DATE;
                RETURN OLD; -- no need since AFTER keyword

        END IF;
END;

$$ LANGUAGE plpgsql;
```

```sql
CREATE TRIGGER scores_log2_trigger
AFTER INSERT OR DELETE OR UPDATE ON Scores
FOR EACH ROW 
EXECUTE FUNCTION scores_log2_func();
```