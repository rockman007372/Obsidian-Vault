
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

Constraints on **WHEN** condition:
- No SELECT (Prevent recursive queries)
- no OLD for INSERT (**OLD = null in INSERT initially**)
- no NEW for DELETE (NEW = null in DELETE)
- ! no WHEN for INSTEAD OF