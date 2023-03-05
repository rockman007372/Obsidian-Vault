![[Pasted image 20230214150258.png]]

- Every entity in a subclass is an entity in the superclass.
- Subclass and superclass may be uniquely identified by the same key. However, subclass key **CANNOT** be shown in ER diagram.
- Each subclass may have additional attributes and relationship. Subclass should **NOT** have the same attributes as the superclass because we can just do queries for these attributes in the superclass.

## Constraints

![[Pasted image 20230214150616.png]]

##### Overlap Constraints

Can a superclass entity belong to _multiple_ subclasses?

-   `TRUE`: A superclass **can belong** to multiple subclasses  
    (e.g., a person can be both student and staff)
-   `FALSE`: A superclass cannot belong to multiple subclasses  
    (e.g., a student is either graduate or undergraduate)

##### Covering Constraints

Must a superclass entity belong to _at least one_ subclasses?

-   `TRUE`: A superclass must belong to at least one subclasses  
    (e.g., there is no student that is neither graduate nor undergraduate)
-   `FALSE`: A superclass need not belong to any subclasses  
    (e.g., not every person is a student or staff)

## ER Mapping

- Most straightforward ISA mapping is the one line relationship (can be neither and can overlap)
- One relation per superclass and subclass.

![[Pasted image 20230214160428.png]]
```sql
CREATE TABLE Persons (
  id    CHAR(20) PRIMARY KEY,
  name  VARCHAR(50)
);

CREATE TABLE Students (
  id    CHAR(20) PRIMARY KEY,
    REFERENCES Persons (id) ON DELETE CASCADE
  year  INT, -- or DATE?
);

CREATE TABLE Grads (
  id      CHAR(20) PRIMARY KEY
    REFERENCES Persons (id) ON DELETE CASCADE,
  phone   INT,
  office  VARCHAR(10)
);
```

Cannot translate other scenarios without using Triggers.