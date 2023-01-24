---
tags: processed
course: CS2102
type: lecture
date: 2023-01-09 Monday
---


## Management

### Database

What is a database: a collection of *organized* data, info and records.

Common challenged:
- Efficiency: **fast** access to **huge** volumn of data
- Transaction: **All of nothing** changes to data (Bank Transfer)
- Data Integrity: **parallel** access and **changes** to data
- Recovery: fast and reliable handling of **failure**
- Security: Fine-grained data access **rights**

### File-Based
- Complex, low level code with similar requirements across diff programs
- High development efforts, many errors

### DBMS 

![[Pasted image 20230117150513.png]]

- Database Management System
- Application logics moved to DBMS
- Have heuristics and blackboxes that process queries commands, we dont need to code them out
- Faster, more stable.

Example Code:

```SQL
SELECT matric, total
FROM FinalMarks
WHERE total >= 93
```

### File-based vs DBMS
You have to code out the file vs typing in commands in DBMS

## Transaction

- A f**inite sequence** of database operations and constitutes the smallest logical unit of work from the app perspective

### Properties 
- each transaction T has ACID properties:
	- Atomicity: either all effects of T are reflected in db or none
	- Consistency: T always yield the correct state
	- Isolation: T is isolated from the effect of concurrent transactions
	- Durability: after a commit of T, its effects are permanent

### Transition graph

- Transition of one state of T to another state of T
- What you will see as a database user is the sequence of **consistent** state depicted in green. In between, the database may go into a _temporary_ inconsistent state. Here, we define consistency as satisfying all user specified constraints.

![[Pasted image 20230117150940.png]]

2 types of transactions: Sequential vs Concurrent → taken care of by DBMS! There is no need to fully understand this. This is simply to illustrate what the database has made easier for us as database user. 

## Serialization

>[!definition]
>- Two executions are **equivalent** if they have the **_same effect_** on the data.
>- A concurrent execution of a set of transaction is **serializable** if this execution is **_equivalent to some_** serial execution of the same set of transactions.

DBMS:
-   Support concurrent executions of transactions to optimize performance
-   Enforce serializability of concurrent executions to ensure integrity of data


## Architecture

3-tier Architecture of DBMS:
- External Schema: users
- Logical Schema: logical organization of data (table, graph, ...)
- Physical Schema: physical organization / storage (disk, memory, files...)

## Relational Model
[[Relational Model]]





## Questions/Cues

---
Links: [[CS2102]]
