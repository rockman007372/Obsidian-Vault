2022-06-29 01:07
Tags: [[Web Development]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
Databases = a structure to store data.

## 2 Types of Databases 

[[SQL]] (Structured Query Language):
- 1 fixed structure
- Eg: MySQL, PostgreSQL

NoSQL (Not only SQL):
- Any format
- Eg: mongoDB, redis 

Comparision between SQL and NoSQL:

![[Pasted image 20220629013209.png]]

## Difference between SQL and NoSQL

### Structure 

SQL: 
- Store data in relational database in the form of tables.
- Cannot add additional info outside the table → must expand table rows/ columns
- Table fills missing table element with null → easy for bugs 
  
![[Pasted image 20220629011441.png|300]]

NoSQL: 
- No structured

![[Pasted image 20230309193712.png]]

### Relationship

SQL can establish relationship between tables through Foreign Key Constraints.

![[Pasted image 20220629012244.png]]

NoSQL can still establish relationship albeit more clumsy:

![[Pasted image 20220629012448.png]]

Depending on data to decide database:
- Data with lots of inter-relationship: SQL
- One single data generating lots of relationship: NonSQL 

### Scalability

- NonSQL is more scalable.
- Traditional SQL databases are designed to handle structured data, and often rely on vertical scaling (adding more resources to a single server to store the database tables)
- NoSQL scales data horizontally by distributing the database across multiple machines or servers (adding more machines or servers to distributed database)
  
  
