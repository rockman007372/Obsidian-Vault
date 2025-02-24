---
tags:
  - toProcess
course: CS4224
type: lecture
date: 2024-09-02 Monday
---

## Notes

#### Intro 

Modern distributed DBMS:
- Data sharding: Partition and distribute huge amt of data accross multiple servers
- Replicate copies for failure resilience

OLAP (Online Analytical Processing)
- Multidimensional  Data Model:
	- model data as a cube
	- STAR schema: fact table and dimension tables
	- obsolete
- Analytical Window Functions

NoSQL System:
- Key-value
- Column family
- Document
- Graph

NewSQL Database System
- Targeted at OLTP workloads
- Features:
	- Relational
	- SQL query language
	- ACID transaction
	- Runs of distributed cluster of shared-nothing nodes

Topics:
1. Data partitioning / fragmentation
2. Storage and Indexing
3. Query Processing and Optimization
4. Transaction Management
5. Data Replication

[[ACID Properties]]

#### Partitioning

How is partitioning done in centralized database system?
- Partition on a key
- SQL function: `PARTITION OF [table] FOR VAlUES FROM [val] to [val]`
- Partitions are mutually exclusive
- Benefits: smaller scans, scan partitions in parallel.

Distributed Database design issues:
- Partitioning/Fragmatation/Sharding: how to partition data into smaller pieces
- Data allocation: how to allocate data to various sites
- Data replication

Data fragmentation
- R => {R1, R2, ..., Rn}
- Each Ri is defined by an Relational Algebra expression on R

Why fragment?
- Locality of access (Asian db vs Europe db)
- Scale horizontally to manage large data
- Improve performance with parallel query execution

Fragmentation Strategies
- Horizontal fragmentation: across different tables
- Vertical: normalized tables
- Hybrid

Desirable properties of fragmentation
- Completeness: each item in R must be found in one of the shards
- Reconstruction: R can be reconstructed from its shards/fragments
- Disjointness:: data items are not replicated (data in each shard is disjoint)
- Balanced: load spreaded accross servers equally

Fragmentation technique:
- Range partitioning
- Hash partitioning
- ! Derived horizontal fragmentation: use the partitioning of the first table to induce the 2nd table??

Hash partitioning:
- Method 1: Modulo
	- May have skewed data, unbalanced shards
- Method 2: Consistent hashing
	- Circular (Ring) cluster of nodes
	- Each node is assigned a hashed value
	- A record t is stored in node N if h(t.A) falls in N's region
	- Supports incremental scaling => minimize data migration when nodes are added/removed
	- Challenges:
		- Non-uniform data and load distribution
		- Oblivious to heterogeneity of servers => should allocate higher load on high-end server
	- Solution: **Virtual nodes**
		- Assign more virtual nodes to higher-end server => increasing the chance of server receiving data => higher-end servers take on higher load
		- Need to maintain table mapping physical servers to virtual nodes

Derived Horizontal Fragmentation
- Partition S in some manner
- Partition R based on the partition of S: Ri = R semi join Si
- Requirement:
	- Completeness: R.A $\subset$ S.A  
	- Disjoint: S.A must be a key (else, many partitions of R may have duplicated R.A values)
	- Hence, R.A must be a foreign key of S with non-null values for R.A
- Benefits:
	- Records often joined together will be stored in the same server (co-located) => reduce join cost

Vertical Fragmentation (Normalization)
- Partition R into {R1, R2...} where 
	- attributes of Ri are subset of R
	- key(R) $\in$ attributes(Ri) => LOSSLESS JOIN PROPERTY

Heuristics for Vertical Fragmentation
- Attribute affinity measure matrix => use clustering algo to decide which attributes go to which vertical partition

Hybrid fragmentation: Combine both

Partitioning considerations:
- Avoid unbalanced data distribution
- Avoid hotspots? (avoid a partitioning key with monotonically increasing values - dates)
	- If we range partition by date, the server that stores the most recent dates will get a lot of XACTs / records
- Optimize for workload's access patterns?
	- Co-locate data that are often accessed (e.g. joined) together
	- Avoid distributed update transactions 
		- e.g. R is hash partitioned on A.
		- XACT: `UPDATE R SET B = B + 1 WHERE C = 20` => update data in multiple nodes/servers
	- Avoid scatter-gather data queries
		- `SELECT * FROM R WHERE B > 20` on R which is has partitioned on A.

## Questions/Cues

