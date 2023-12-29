A lossless join is a database design concept that ensures that no data is lost when two or more relations/tables are combined using a common attribute or key. 

In other words, a lossless join guarantees that the original data can be reconstructed from the smaller tables after decomposition.

>[!Condition]
> A lossless join is guaranteed if the common attributes form a **superkey** of **at least one** of the smaller tables.

For example, R(A, B, C, D) decomposed into R1(A, B, C) and R2(B, C, D), where {B, C} is a superkey of R1.  Hence R1 and R2 form a loss-less join decomposition.


>[!Condition]
> A decomposition is lossless iff the common attributes in the smaller tables form a **superkey** of **at least one** of the smaller tables.