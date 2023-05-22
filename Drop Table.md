## Drop Table

```SQL
DROP TABLE
	[IF EXISTS] -- no error if table does not exist
	<table_name>[, <table_name> [, <table_name> [...]]] -- multiple table
	[CASCADE]; -- also delete referencing table
```