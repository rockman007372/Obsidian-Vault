4 operations in [[Relational Model]] database:
- Projection
- Selection
- Group By and Aggregation
- Join

We can implement them using [[MapReduce]].

## Implementation

To implement [[Projection]]:
- Map takes in a tuple and emits a new tuple with specified attributes
- No need reducer

To implement [[Selection]]:
- Map takes in a tuple and emits if it satisfies the conditions
- No reducer

To implement Group By + Aggregation:
- Map takes in a tuple, and emit its (key, value).
- Framework groups these tuples by key in the shuffle phase.
- Reducer computes aggregate of the tuples of the same key.
- Can be optimized with combiners!

To implement [[Inner Join]], we have 2 methods:

1. Broadcast Join

- Each mapper stores a copy of the small table in the form of a hash table.
- Each mapper iterates over a split of the bigger table, joining each tuple with the ones in the smaller table.

![[Pasted image 20230923144345.png]]

2. Reduce-side Join

- Each mapper works on one table, emiting records with a composite key (key, table_id)
- Each reducer works on one (original) key. We use the secondary key table_id to **make sure keys from table X arrive before table Y.** 
- Each reducer then holds the keys from table X in memory and **cross** them with records from table Y.

![[Pasted image 20230923144610.png]]

![[Pasted image 20230923145105.png]]





