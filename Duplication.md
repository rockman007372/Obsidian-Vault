How to do join operations in NoSQL databases?
- Design tables in advance around queries we expect to receive. Best to process fixed types of queries.
- This leads to duplicated information, which is ok becaues storage is cheap in distributed file storage.
- However, how to ensure consistency among tables? (e.g. change data in one table, what happens to data in the joined table?)