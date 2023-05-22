---
tags: processed
course: CS2102
type: lecture
date: 2023-03-19 Sunday
---

In PL/pgSQL, a trigger is a special kind of function that is **automatically invoked in response to certain events** on a table, such as inserting, updating, or deleting a row. When a trigger is fired, it can execute PL/pgSQL code to perform additional actions or validations.

A trigger function, on the other hand, is a **regular PL/pgSQL function** that is called by a trigger. It is the code that is executed when a trigger is fired, and it typically includes SQL statements that modify data or perform some other task.

## Example

See [[Examples of Triggers in PL-PGSQL]]

## Content

1. [[Trigger Timing]]
2. [[Return Values of Trigger Function]]
3. [[INSTEAD OF Trigger]]
4. [[Trigger Levels]]
5. [[WHEN Condition in Triggers]]
6. [[Deferred Trigger]]
