---
tags: sql
aliases: PL/pgSQL
date: 2023-03-11 Saturday
course: CS2102
type: lecture
---
Links: [[CS2102]]
- - -

PL/pgSQL is a **procedural language** extension for [[PostgreSQL]]. It provides a set of features that enable the creation of complex database **functions, triggers, and stored procedures.**

Benefits:
- Move application logic and calculations to the database itself => better performance + code maintenance
- Database operations grouped as a "single unit" => ensure consistency, "all-or-nothing" behaviour.

Content:
- [[Structure of PL-pgSQL functions]]
- [[Stored Functions in PL-pgSQL]]
- [[Stored Procedures in PL-pgSQL]]
- [[Control Structure in PL-pgSQL]]

## Common questions

1. Differences between functions and procedures:
- Functions must return something (even void), but procedures do not have to.
- Functions can be called in [[Data Manipulation Language|DML]] (SELECT, INSERT, UPDATE, DELETE) but Procedures cannot.
- Procedures can commit or rollback transactions during execution, functions cannot.
- Procedures can be invoked in isolation using `CALL`. Function must be invoked in `SELECT` statement.

