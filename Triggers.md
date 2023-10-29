---
tags: processed
course: CS2102
type: lecture
date: 2023-03-19 Sunday
---

Trigger: 
- a special kind of function that is **automatically invoked in response to certain events** on a table, such as inserting, updating, or deleting a row. 
- When a trigger is fired, it can execute PL/pgSQL code to perform additional actions or validations via a **trigger function**.

Trigger function:
-  a **regular PL/pgSQL function** that is called by a trigger. 
- It is the code that is executed when a trigger is fired, and it typically includes SQL statements that modify data or perform some other task.

## Basic template

![[Pasted image 20231024205405.png]]
## Content

1. [[Examples of Triggers in PL-PGSQL]]
2. [[Trigger Timing]]
3. [[Return Values of Trigger Function]]
4. [[INSTEAD OF Trigger]]
5. [[Trigger Levels]]
6. [[WHEN Condition in Triggers]]
7. [[Deferred Trigger]]
