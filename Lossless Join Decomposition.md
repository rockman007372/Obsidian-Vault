A lossless join is a database design concept that ensures that no data is lost when two or more relations (database tables) are combined using a common attribute or key. 

In other words, a lossless join guarantees that the original data can be reconstructed from the smaller tables after decomposition.

>[!Condition]
> A lossless join is guaranteed if the common attribute is a **superkey** of **at least one** of the smaller tables.

For example, R1 and R2 form a loss-less join decomposition when the common attributes in R1 and R2 constitute a **superkey** of R1 **or** R2.

Example:
- R(A, B, C, D) decomposed into R1(A, B, C) and R2(B, C, D), where {B, C} is a superkey of R1. 