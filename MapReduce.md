MapReduce is a programming model and processing technique for distributed data processing.

It is commonly used in big data processing frameworks like Apache [[Hadoop]]. It is designed to process and generate large datasets that can be distributed across a cluster of computers. 

A MapReduce program consists of two main stages:

1. **Map Stage:** 
- The input data is divided into smaller chunks, called splits, and each split is processed by a map function. 
- The map function takes the input data, processes it, and generates a set of key-value pairs as intermediate output. ("map outputs.") 
- The map function is typically designed to perform some filtering, sorting, or transformation of the data.

2. **Reduce Stage:** 
- After the map stage, the intermediate key-value pairs are grouped together based on their keys, and each group is processed by a reduce function.
- The reduce function takes a group of key-value pairs with the same key and performs some aggregation or computation on them to produce the final output. 
- The reduce function's output is typically written to an external storage system or used for further analysis.


## Other steps to take note

- **Partition step**: decides which reducers take on which key. 
	- By default, decided by a hash function. 
	- User can implement custom partition to spread out load among reducers.
- **Combiner step**: "mini-reducers", locally aggredate output from **mappers** so reducers can take on fewer loads.
	- User's responsible for ensuring correctness
	- Reducer can be used as combiners when operation is both *associative* and *commutative*.
		- associative: a + (b + c) = (a + b) + c
		- commutative" a + b = b  + a