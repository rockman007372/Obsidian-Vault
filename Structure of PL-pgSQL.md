## Structure of PL/pgSQL

```plsql
CREATE FUNCTION somefunc(integer, text) RETURNS integer
AS $$function_body_text$$
LANGUAGE plpgsql; -- note the LANGUAGE used here
```

Note:
- The function body is simply a string literal so far as `CREATE FUNCTION` is concerned.
- `CREATE FUNCTION` is a standard SQL statement that is part of the SQL language. 
- Function body syntax varies according to the LANGUAGE specified.

PL/pgSQL is a block-structured language. The complete text of a function body must be a _block_. A block is defined as:

```plsql
[<< label >>] -- [] means optional
[DECLARE
	declarations;] -- declare variable names
BEGIN
    statements;
END [label];
```

A _`label`_ is only needed if you want to:
- identify the block for use in an `EXIT` statement (Optional), or 
- to identify the names of the variables declared in the block. 

Example code:

```sql
CREATE FUNCTION somefunc() RETURNS integer AS $$
<< outerblock >>
DECLARE
    quantity integer := 30;
BEGIN
    RAISE NOTICE 'Quantity here is %', quantity;  -- Prints 30
    quantity := 50;
    
	<< subblock >>
    DECLARE
        quantity integer := 80;
    BEGIN
        RAISE NOTICE 'Quantity here is %', quantity; -- 80
        RAISE NOTICE 'Outer quantity here is %', outerblock.quantity; -- 50
    END;
    
    RAISE NOTICE 'Quantity here is %', quantity; -- 50
    RETURN quantity;
END;
$$ LANGUAGE plpgsql;
```