- A data model that stores associations between keys and values.
- Keys are usually primitives and can be queried
- Values can be primitive or complex, cannot be queried usually (JSON, HTML fragment, BLOB...)
- Very simple API: 
	- Get 
	- Put
- Suitable for:
	- Small continuous read and writes
	- Storing basic information with no clear schema
	- When complex queries are not required
- Example:
	- Storing user sessions
	- Caches
	- User data processed individually (e.g. patient medical data => personal)

## Implementation

- Non-persistent: Stored in memory as hash table
- Persistent: Stored persistently in disk
