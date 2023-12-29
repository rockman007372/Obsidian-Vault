---
tags: 
aliases:
  - RDD
date: 2023-10-28 Saturday
---
Links: 
- - -

RDD stands for **Resilient Distributed Dataset**, and it is one of the core data structures in [[Apache Spark]].

#### Key characteristics

- **Distributed Dataset:** Collections of **objects** that are distributed over machines.
- **Resilient:** If a partition of an RDD is lost due to a node failure, Spark can recompute the lost partition using the lineage information (the sequence of transformations on the original data).
- **Immutable**
- **Lazy Evaluation:** transformations on RDDs are not executed immediately. Instead, they are recorded and executed only when triggered by actions.
- **Cacheable:** RDDs can be explicitly cached in memory, allowing Spark to persist the data across multiple operations. This can significantly speed up iterative algorithms or interactive data analysis.

#### Example

```python

# each worker read file in parallel
lines = sc.textFile(“hdfs://...”) 

# transformation
errors = lines.filter(lambda s: s.startswith(“ERROR”)) 
messages = errors.map(lambda s: s.split(“\t”)[2]) 

# cache the messages block to memory
messages.cache() 

messages.filter(lambda s: “mysql” in s).count() 

# this queries run much faster
messages.filter(lambda s: “php” in s).count()
```

Note:
- Cache is also a transformation.
- Since memory is limited, worker node will evict least-recently-used RDDs.

#### Tranformation DAG 

![[Pasted image 20231028152914.png]]

```python
val file = sc.textFile(“hdfs://...”) 

val counts = file.flatMap(line => line.split(“ ”)) 
	.map(word => (word, 1)) 
	.reduceByKey(_ + _) 

counts.save(“...”)
```

![[Pasted image 20231028153206.png]]

Narrow Dependency:
- Map-like transformation (map, flatmap, filter, contains...)
- Each worker does not need to communicate with each other 

Wide Dependency:
- Reduce-like transformation (reduceByKey, groupBy, orderBy...)
- Data needs to be shuffled accross partitions similar to shuffling stage in map-reduce.

Stages:
- Consecutive **narrow** dependencies are group together as stages
- Within stages, data are transformed on the same machine
- Accross stages, intermediate data are shuffled and **automatically written onto local disks** ⇒ if node is down, no need to compute intermediate results and shuffle again.
- ? does it write to local disk or ram

It is the programmer's responsibility to minimize wide-dependency.

#### Lineage Approach

If a worker node goes down, we replace it by a new worker node, and use the graph (DAG) to recompute the data in the lost partition.