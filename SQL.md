---
tags: processed
course: CS2102
type: info
date: 2023-01-09 Monday
---

## What is SQL
Structured query language (SQL) is a programming language for storing and processing information in a relational database (See relational database in [[Relational Model]]). 

A relational database stores information in tabular form, with rows and columns representing different data attributes and the various relationships between the data values. 

You can use SQL statements to store, update, remove, search, and retrieve information from the database. You can also use SQL to maintain and optimize database performance.

## What are the components of a SQL system?

Relational database management systems use structured query language (SQL) to store and manage data. The system stores multiple database tables that relate to each other. MS SQL Server, MySQL, or MS Access are examples of relational database management systems. The following are the components of such a system. 

### **SQL table**

A SQL table is the basic element of a relational database. The SQL database table consists of rows and columns. Database engineers create relationships between multiple database tables to optimize data storage space.

For example, the database engineer creates a SQL table for **products** in a store: 

| **Product ID** | **Product Name** | **Color ID** |
| -------------- | ---------------- | ------------ |
| 0001           | Mattress         | Color 1      |


Then the database engineer links the **product** table to the **color** table with the _Color ID:_

| **Color ID** | **Color Name** |
| ------------ | -------------- |
| Color 1      | Blue           |
| Color 2      | Red            | 

### **SQL statements**

SQL statements, or SQL queries, are valid instructions that relational database management systems understand. Software developers build SQL statements by using different SQL language elements. SQL language elements are components such as identifiers, variables, and search conditions that form a correct SQL statement.

For example, the following SQL statement uses a SQL INSERT command to store _Mattress Brand A,_ priced _$499,_ into a table named _Mattress_table,_ with column names _brand_name_ and _cost:_

```
INSERT 
INTO Mattress_table(brandName, cost)
VALUES(‘A’,’499’);
```

### **Stored procedures**

Stored procedures are a collection of one or more SQL statements stored in the relational database. Software developers use stored procedures to improve efficiency and performance. For example, they can create a stored procedure for updating sales tables instead of writing the same SQL statement in different applications.


## What is PostgreSQL
PostgreSQL is a powerful, open source object-relational database system that uses and extends the SQL language combined with many features that safely store and scale the most complicated data workloads.

---
Links: 

