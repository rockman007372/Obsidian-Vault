2022-06-29 01:07
Tags: [[Web Development]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Databases
### Main Points
Databases = a structure to store data.

Comparision between SQL and NoSQL:
![[Pasted image 20220629013209.png]]

#### 2 types of Databases 
- SQL: Structured Query Language - 1 fixed structure
	- MySQL, PostgreSQL
- NoSQL: Not only SQL - any format
	- mongoDB, redis 

#### Difference between SQL and NoSQL
##### 1. Structure: 
SQL: 
- store data in sequelled database in the form of tables? 
![[Pasted image 20220629011441.png|300]]
- Cannot add additional info outside the table -> must expand table rows/ columns
- Table fills missing table element with null -> easy for bugs 
  
NoSQL: 
- No structured

##### 2. Relationship
SQL can establish relationship between tables:
![[Pasted image 20220629012244.png]]

NoSQL can still establish relationship albeit more clumsy:
![[Pasted image 20220629012448.png]]

Depending on data to decide database:
- Data with lots of inter-relationship: SQL
- One single data generating lots of relationship: NonSQL 

##### 3. Scalability
- NonSQL is better when data increases
- SQL is slower - costly to scale vertically on one computer
- NoSQL scales data in a distributive system - scale horizontally on many computers
  
  
