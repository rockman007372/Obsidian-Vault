
>[!definition]
> A primary key is a selected candidate key.

We <u>underline</u> the primary key in the schema notation:

  >[!example]
  > Movies(<u>id: INT</u>, title: **TEXT**, genre: **TEXT**, opened: **DATE**)
  
## Primary Key Constraints

>[!Constraint]
> A primary key must satisfy the followings:
> - Uniquely identifies a tuple in a relation.
> - Primary key attributes cannot be NULL.