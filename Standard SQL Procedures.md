```sql
CREATE OR REPLACE PROCEDURE transfer(
	fromAcct TEXT, 
	toAcct TEXT, 
	amount INT
) AS $$

  UPDATE Accounts  
  SET balance = balance - amount  
  WHERE name = fromAcct;

  UPDATE Accounts  
  SET balance = balance + amount  
  WHERE name = toAcct;

$$ LANGUAGE sql;

-- To execute the procedure above:
CALL transfer('Alice', 'Bob', 100);
```