---
tags: toProcess
course: CS2102
type: meeting
date: 2023-08-17 Thursday
---
## People missing

### 31 Aug
chee teng


### 7 Sep
bai zhou
yong ning
shaun

## Meeting minutes

- Attendance compulsory. 1 mark deducted per tut missed. 2 grace tutorials, anymore we deduct.
- No participation mark
- Not more than 45 min per tut
- weekly meeting on the next tutorial - 5pm Tuesday
- Book used: fundamentals of database systems
- Chapter covered: 3, 4, 9, 14, 15
- Online postgres: https://dbfiddle.uk/btGcOH30
- MC sent to who?

### Exam
- Midterm: Chapter 1 to 5

## Tutorial 3

Q1.
- DISTINCT unnecessary, department is PK
- Must have alias of table name

Q2.
- Need DISTINCT
- Must query from student table

Q3.
- Get students who violate constraint: borrow books before joining university
- Both DISTINCT and no DISTINCT acceptable

Q4. manipulate NULL values
- Select (...) as duration is not seen in lecture
- returned IS NOT NULL = NOT (returned IS NULL)
- ! loan must have an alias!!

Q5. crazy minion query long
- No need copy table, only allowed to do if we know foreign key constraint
- loan references copy, copy references book => can go straight to book
- may decide to mark down queries if its not simplified?? Performance matters

Q2a.
- INNER JOIN and ON

Q2b.
- UNION and EXCEPT and INTERSECT



---
Links: [[CS2102]]
