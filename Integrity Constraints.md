>[!Principle of Rejection]
>Reject the insertion if the condition evaluates to **False**

Take note of [[Three-Valued Logic]]:
- IS NULL operation
- IS DISTINCT FROM operation = not equivalent 

## Integrity Constraints
- [[Ways to Specify SQL Constraints]]
- [[Types of SQL Constraints]]
- [[Deferrable Constraints]]

## Summary 

![[Pasted image 20230204233222.png]]

>[!Attention]
> Remember, the condition must be False for the insertion to be rejected. If it is NULL, then the insertion will still be performed (eg. NULL > 30 == NULL)

