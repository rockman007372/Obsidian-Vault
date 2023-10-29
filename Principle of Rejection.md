
>[!Principle of Rejection]
>Reject the insertion if the condition evaluates to **False**

Take note of [[Three-Valued Logic]]:
- IS NULL operation
- IS DISTINCT FROM operation = not equivalent 

>[!Attention]
> - Remember, the condition must be False for the insertion/update/delete to be rejected. 
> - If attribute is NULL, then the insertion may still be performed (eg. (NULL > 30 == NULL) ⇒ inserted)