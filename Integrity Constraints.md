In SQL, an integrity constraint is a rule that ensures the accuracy and consistency of data in a database. It is used to maintain the validity and reliability of the data stored in tables.

## Principle of rejection

>[!Principle of Rejection]
>Reject the insertion if the condition evaluates to **False**

Take note of [[Three-Valued Logic]]:
- IS NULL operation
- IS DISTINCT FROM operation = not equivalent 

>[!Attention]
> - Remember, the condition must be False for the insertion/update/delete to be rejected. 
> - If attribute is NULL, then the insertion may still be performed (eg. (NULL > 30 == NULL) ⇒ inserted)

## SQL constraint specification in SQL

See  [[SQL Constraint Specification]]


## Types of Integrity Constraints in SQL

See [[5 Types of SQL Constraints]]

## Deferable Constraints

See [[Deferrable Constraints]]

# Summary 

![[Pasted image 20230204233222.png]]



