
Good:
- No update or deletion or insertion anomalies
- Small redundancy
- Guarantees [[Lossless Join Decomposition]].
	- Why? After decomposition,  R1 contains all attributes in X+, which makes X the superkey of R1. R2 contain X, and the remaining attributes not in X+.
	- Since X is the common attribute in both decomposed tables and it is a superkey of at least one of them, the decomposition is lossless join.

Bad:
- BCNF has no [[Dependency Preservation]].

### Example of dependency loss

Table R(A, B, C) with AB → C and C → B

![[Pasted image 20230421132722.png]]

Keys = {AB}, {AC}

BCNF decomposition: 

- R1(A, C)
- R2(B, C) 

The functional dependency AB → C cannot be retrieved from R1 and R2.

Hence BCNF decomposition may not always preserve all FDs.


