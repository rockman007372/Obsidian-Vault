Format:

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE some_column = some_value;
```

Example:

```sql
UPDATE orders
SET status = 'Shipped', ship_date = '2023-03-18'
WHERE order_id = 123;
```

For each of the orders with id 123, update their status and ship date.