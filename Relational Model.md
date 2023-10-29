---
tags: processed
course: CS2102
type: lecture
date: 2023-01-17 Tuesday
---
- Based on [[Relation]] concepts. 
- All data are organised in terms of their relations to each other.

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
>A relation is a set of tuples.

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

### Data Integrity

Conditions that restrict what constitutes valid data.

**Structural constraints:**
- Independent of application
- Domain constraints (Cannot store TEXT in INT column)
- [[Key Constraints]]
- [[Foreign Key]]

>[!misconception]
> Key constraints are not an intrinsic property of a relation. They are designed by the database engineer to define what constitutes valid data

**General constraints:**
- Dependent on application
- *Check constraints*
- Triggers?

