---
tags: processed
course: CS2102
type: content
date: 2023-01-17 Tuesday
---

## History

- Hierachical model: high to low rank, tree → no overlapping of children
- Network model
- **Relational Model:** All data are organised in terms of their relations to each other
	- Commercial RDBMS
	- Open-Source RDBMS
- Object-Oriented Model:
- More Recent Development:
	- NoSQL Model
	- In-Memory DBMS


## Relational Model

Based on [[Relation]] concepts.

### Relation Schema
- A schema is the **definition** of a relation.
- Specifies the attributes (columns) and data constraints (domain constraints)
- It is the framework of a table (but not an instance of a table yet)
- Simplified notation of a relation schema where the domain is clear from context is $R(A_1, A_{2}, ...,A_{n})$

```SQL
Employees(id: INT, name: TEXT, dob: DATE, salary: NUMERIC)
```

### Domain

>[!Definition]
> A domain is a set of atomics.
> - Atomic means indivisible values (int, numeric, text)
> - domain of attribute $A_i$ is $dom(A_i)$ = The set of possible values of $A_i$
> - Each value v of attribute $A_i$ is either $v = NULL$ or $v \in dom(A_{i})$
> 

### Relation

>[!definition]
>A relation is a set of tuple.

- A relation is basically a table - an instance of the relation schema. 
- Each **instance** of schema R is a relation which is a subset of $$\set{(a_{1}, a_{2},...,a_{n}) \text{ | } a_{i} \in dom(A_{i}\cap \set{NULL}}$$
- $R.A_i$ referes to the attribute $A_i$ of relation R

Example:

![[Pasted image 20230117153837.png]]

```SQL
Modules(course: TEXT, mc: INT, exam: BOOL)

dom(course) = {cs2102, cs3223, cs4221}
dom(mc) = {2, 4}
dom(exam) = {yes, no}
```

The table above is an instance of the schema Modules, which is a subset of:

`{cs2102, cs33223, cs4221, NULL} x {2, 4, NULL} x {yes, no, NULL}`

### Relational Database Schema

- Relational Database Schema is set of relation schemas + data constraints
- A relational database is a collection of tables

Examples:

```SQL
Movies(
	id: INT
	title: TEXT
	genre: TEXT
	opened: DATE
)

Casts(
	movie_id: INT
	actor_id: INT
	role: TEXT
)
```

![[Pasted image 20230117155015.png]]

## Data Integrity

- Conditions that restrict what constitutes valid data

### Structural
- Independent of application
- Domain constraints (Cannot store TEXT in INT column)
- Key constraints
- Foreign key constraints

### General
- Dependent on application
- Check constraints
- Triggers?

## Key Constraints

### Superkey

>[!definition]
> A superkey is a subset of attributes that **uniquely** identifies a tuple in a relation

### Key

>[!definition]
> A key is a **superkey** that is also **minimal**

- Minimal (cannot be made smaller) != minimum
- No proper subset of the key is a superkey (eg: if (A, B, C) is a key then (A, B) cannot be a superkey)

**Properties**
-   If _(A, B, C)_ is _definitely_ a **_superkey_** then _(A, B, C, D)_ is a **_superkey_** → recursive 
-   If _(A, B, C)_ is _definitely_ a **_key_** then _(A, B, C)_ is a **_superkey_**  → definition
-   If _(A, B)_ is _definitely_ a **_superkey_** then _(A, B, C)_ is **NOT** a **_key_** → _(A, B, C)_ is not minimal!
-   If _(A, B)_ is _definitely_ a **_key_** then _it is possible that_ _(B, C)_ is also a **_key_**  
-   Every relations have at least 1 superkey 

**Example:**

Consider a forum database with the following relation filled with many thousands of users: _Accounts(email: **TEXT**, password: **TEXT**, name: **TEXT**)_.

Using reasonable guess, which subsets of attributes are **superkeys** of relation _Accounts_?

**Answer:**

{email} = key
{password} = key
{email, password} = superkey (not minimal)

### Candidate Keys

>[!definition]
>The candidate keys is the set of **all keys** of a given relation.

### Primary Key

>[!definition]
> A primary key is a selected candidate key.

- Primary key attributes cannot be NULL
- We <u>underline</u> the primary key in the schema notation:
  
  > Movies(<u>id: INT</u>, title: **TEXT**, genre: **TEXT**, opened: **DATE**)

![[Pasted image 20230117185739.png]]


### Prime Attributes

- A prime attribute is one of the attributes that make up the candidate keys. 
- It can also be used to uniquely identify a tuple in the schema.

### Differences between Candidate Keys and Primary Key

- Candidate keys are the attributes that could be the primary key
- The primary key is an attribute that uniquely identifies the row (a tuple in the relation)

## Foreign Key Constraints

### Foreign Key

>[!definition]
> A foreign key is a subset of attributes of relation R1 that refers to the **primary key** of relation R2

We say that:
- R1 is the **referencing** relation
- R2 is the **referenced** relation

>[!Notes]
>-   A **_referencing relation_** can be a **_referenced relation_** for different foreign key  
>- The **_referencing relation_** and the **_referenced relation_** can be the same relation


![[Pasted image 20230117193618.png]]

In the tables above, we have: (Cast.actor_id) ⇝ (Actors.id) 
- actor_id is foreign key in Cast and Cast is the referencing relation.
- id is primary key in Actors and Actor is the referenced relation.

### Constraints

**Foreign key constraints** are the rules created when we add foreign keys to a table. 

Each foreign key in R1 must satisfy one of the following:
- Appear as primary key in R2 (meaning it must **exist** in R2) or
- Be a NULL value (or a tuple containing at least one NULL value)

### Differences between Primary and Foreign Key

- A primary key value must be unique, and cannot be NULL.
- ? A foreign key value does not have to be unique, and can be NULL

## Misconceptions

- Key constraints are not an intrinsic property of a relation
- They are designed by the database engineer to define what constitutes valid data.

## Summary

![[Pasted image 20230117205308.png]]