
We can decompose the table into smaller tables (Normalization)

![[Pasted image 20230401205330.png]]

Algorithm:

1. Find a closure $X^+$ that violates **more but not all**
2. Decompose R into two tables R1 and R2, such that
	- R1 contains all attributes in ${X}^+$
	- R2 contains all attributes in $X$ as well as the attributes not in ${X}^+$
3. Repeat if any decomposed table is not in BCNF

Note:
- ! If a table has only 2 attributes, it must be in BCNF ⇒ Prioritise table with 2 attributes during decomposition/normalization
- BCNF decomposition may not be unique

Sometimes a decomposed table R1 may have hidden FDs that are not obvious:

>[!example]
> Given table R with FD A → B, BC → D.
> 
> ![[Pasted image 20230401211031.png]]

**Problem**: we dont know what FDs exist in R2, because R2 does not have attribute B.

**Solution**: Derive the closure on R, then project them onto R2.

1. Find all the subsets of R2 attributes.
2. For each subset, find its closure on R (including attributes **not** in R2)
3. Remove the extra attributes from the closure and check for violation.

In R, {AC}+ = {A, B, C, D}. After projecting onto R2, {AC}+ = {A, C, D}, which violates more-but-not-all rule. Hence R2 is not a BCNF.