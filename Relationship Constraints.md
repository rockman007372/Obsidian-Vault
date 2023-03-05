## Cardinality

- Upper-bound
- Upper limits of 1 = [[Key Constraints]]
- 3 types of cardinality relationship:
	- Many-to-Many
	- Many-to-One
	- One-to-One

![[Pasted image 20230214140819.png]]


## Participation

- Lower-bound
- Lower limits of 0 are called **partial participation constraints**
- Lower limits of 1 are called **total participation constraints**

![[Pasted image 20230214140847.png]]

## Key + Total Participation

- Key + total participation constraint = must have a relationship with exactly **one** entity.

![[Pasted image 20230214141021.png]]

## Dependency

- **Weak entity sets** are entity sets that do not have its own key (its key are called partial keys)
- Must have **identifying relationship set** connecting to the owner entity set.

>[!Example]
> A book chapter is dependent on a book.

![[Pasted image 20230214141255.png]]

Note:
- Each chapter must be connected to a book.  -> Weak entity set must have **total participation constraint** in the identifying relationship.
- Each chapter can only belong to one book -> **Many-to-one key constraint** from weak entity set to owner entity set.
- The attribute `num` is not enough to uniquely identify chapter, hence it is a partial key. The set `{name, num}` is thus a (primary) key of chapter.

# Summary

![[Pasted image 20230214141058.png]]