Example:

```sql
CREATE TRIGGER scores_log_trigger
AFTER INSERT ON Scores
FOR EACH ROW EXECUTE FUNCTION scores_log_func();
```

Trigger timing allows you to detemine when to activate the trigger:
- `AFTER <OP>`
- `BEFORE <OP>`
- `INSTEAD OF <OP>`: trigger function is executed *instead of* the operation.