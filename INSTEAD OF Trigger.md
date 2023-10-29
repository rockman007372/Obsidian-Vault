#### Use case
- Only defined on `VIEWS`.
- Instead of performing operation on a view (virtual table), do it on the actual table instead.

#### Example
We have a view `Max_Score`:

```sql
CREATE OR REPLACE VIEW Max_Score AS
     SELECT * FROM Scores 
     ORDER BY Mark DESC 
     LIMIT 1;
```

Whenever someone wants to update the view `Max_Score`, we update the corresponding tuple in Scores instead.

```sql
CREATE TRIGGER update_max_trigger
INSTEAD OF UPDATE ON Max_Score
FOR EACH ROW 
EXECUTE FUNCTION update_max_func();
```

```sql
CREATE OR REPLACE FUNCTION update_max_func() RETURNS TRIGGER AS $$

-- Updating the table will update the view dynamically
BEGIN
        UPDATE Scores
        SET Mark = NEW.Mark WHERE Name = OLD.Name; 
        RETURN NEW; -- must return non-null values so operation proceeds
END;

$$ LANGUAGE plpgsql;
```

Note:
- ! Returning `NULL` signals database to ignore the rest of the operations on the current row
- Return non-null tuple signals db to proceed as normal