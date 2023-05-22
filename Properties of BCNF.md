
Good:
- No update or deletion or insertion anomalies
- Small redundancy
- ! The original table can always be reconstructed from the decomposed table. In other word, the decomposition guarantees [[Lossless Join Decomposition]].
	- Why? After decomposition,  R1 contains all attributes in X+, which makes X the superkey of R1.
	- The decomposition guarantees a lossless join whenever the common attributes in R1 and R2 forms a superkey in either R1 or R2 or both.

Bad:
- ? Some dependencies are not preserved. In other word, BCNF has no [[Dependency Preservation]].

### Example of dependency loss

Table R(A, B, C) with AB -> C and C -> B

![[Pasted image 20230421132722.png]]

Keys = {AB}, {AC}

BCNF decomposition: 

- R1(A, C)
- R2(B, C) 

The functional dependency AB -> C cannot be retrieved from R1 and R2.

Hence BCNF decomposition may not always preserve all FDs.


