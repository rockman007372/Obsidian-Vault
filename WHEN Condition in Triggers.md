
Use `WHEN` condition in triggers to specify which cases will activate the triggers.

```sql
CREATE OR REPLACE FUNCTION for_Elise_func() RETURNS TRIGGER AS $$
BEGIN
        NEW.Mark := 100;
        RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

```sql
CREATE TRIGGER for_Elise_trigger
BEFORE INSERT ON Scores
FOR EACH ROW
WHEN (NEW.Name = 'Elise') -- TRIGGER COND, after FOR EACH
EXECUTE FUNCTION for_Elise_func();
```

#### Caveats

There are restrictions on the `WHEN` condition:
- The `WHEN` condition cannot include a subquery (no `SELECT` clause)
- Cannot call `OLD` for `INSERT` (OLD = null in INSERT initially)
- Cannot call `NEW` for `DELETE` (NEW = null in DELETE)
- ! Cannot use `WHEN` clause for `INSTEAD OF`