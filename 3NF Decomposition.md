
A 3NF decomposition has only one split, which divides the table into 2 or more parts.

![[Pasted image 20230421165212.png]]

Compared this to [[BCNF Decomposition]], which performs multiple binary splits.

![[Pasted image 20230421165345.png]]

### Algorithm

Given a table R and a set S of [[Functional Dependency]]

1. Derive a [[Minimal Basis]] of S
2. In the minimal basis, combine the FDs whose **left-hand sides** are the same.
3. Create a table for each FD remained.
4. ! If none of the tables contains a key of the original table R, create a table that contains a key of R (any will do) ⇒ ensure lossless join decomposition
5. Remove redundant table (if all the attributes in a table are contained in another table)

### Example 

Table R(A, B, C, D) with S = { A → BD, AB → C, C → D, BC → D } 

1. Minimal basis S' = {A → B, A → C, C → D}
2. Combine FDs whose left-hand sides are the same: S' = {A → BC, C → D}
3. Create tables: R1(A, B, C), R2(C, D)
4. Since R1 contains A, which is the key of the original table, no need to insert additional table.