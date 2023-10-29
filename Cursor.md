---
tags: sql, plpgsql
aliases: 
date: 2023-03-11 Saturday
---

A cursor enables us to access each individual row returned by a SELECT statement in SQL.

Motivation:
- Allow access to individual rows without executing the whole query to get a complete result.
- Avoid memory overrun when query result is large.

The cursor workflow is as followed:

![[Pasted image 20230311183438.png]]

Variations of `FETCH`:
- `FETCH curs INTO record`: retrieve a tuple from Cursor `curs` to Record `record`
- `FETCH PRIOR FROM curs INTO record`: fetch the prior tuple
- `FETCH FIRST FROM curs INTO record`: fetch first tuple in table
- `FETCH LAST FROM curs INTO record`: fetch last tuple in table
- `FETCH ABSOLUTE 3 FROM curs INTO record`: fetch the 3rd tuple

### Example

>[!question]
> Write a function to sort the students in descending order of their Marks. **For each student, compute the difference between his/her mark and the previous student.** 

![[Pasted image 20231018123500.png]]