>[!definition]
> A foreign key is a subset of attributes of relation R1 that refers to the **primary key** of relation R2

We say that:
- R1 is the **referencing** relation
- R2 is the **referenced** relation

>[!Notes]
>-   A **_referencing relation_** can be a **_referenced relation_** for different foreign key  
>- The **_referencing relation_** and the **_referenced relation_** can be the same relation (Self-referencing)


![[Pasted image 20230117193618.png]]

In the tables above, we have: (Cast.actor_id) ⇝ (Actors.id) 
- *actor_id* is *foreign key* in Cast and Cast is the referencing relation.
- *id* is *primary key* in Actors and Actor is the referenced relation.

A foreign key must follow [[Foreign Key Constraint]].

## Differences between Primary and Foreign Key

- A primary key value must be unique, and cannot be NULL.
- ? A foreign key value does not have to be unique, and can be NULL