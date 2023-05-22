
- Also include tuples that do not satisfy the condition.
- Why? Sometimes a tuple in R or S that do not match are also of interest (dangling tuple)

**Informal Steps**
1. Perform inner join M = R $\Join$ S
2. Add dangling tuples to M from:
	- R in case of a **left** outer join - ⟕
	- S in case of a **right** oter join -  ⟖
	- R and S in case of a **full** outer join - ⟗
3. Pad missing attribute values of dangling tuples with NULL.

**Examples**

>[!example]
> Find all the employees not assigned to any project

![[Pasted image 20230123164446.png]]

- The dangle tuples are those where employees' names do not match ename.
- In those tuples, the ename will be assigned NULL.
- ! Pay attention to which relation comes first.