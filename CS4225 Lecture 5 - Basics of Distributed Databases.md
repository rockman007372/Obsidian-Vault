---
tags: []
course: CS4225
type: lecture
date: 2023-09-28 Thursday
---
We focus on how NoSQL systems are implemented as distributed databases.

## Basic Concepts of Distributed Databases

Motivation:
- Scalability: database scale horizontally by adding more nodes.
- Availability: if one node fails, others can still handle requests.
- Latency: each request is handled by the closest node.

Abstraction: 
- users need not know how data is distributed, as long as request is handled.

Assumptions: 
- All nodes are well-behaved (no adversarial nodes, unlike blockchains)

Architectures:

![[Pasted image 20231028110639.png]]
- Shared everything: single-node DBMS
- Shared memory: Supercomputers
- Shared disk: Cloud database
- ! Shared nothing: NoSQL (e.g. MongoDB)

### Partitioning 

How to partition data among nodes (machines)?

- Table partitoning: Store different tables in different nodes => bad idea, cannot scale
- ! Horizontal Partitioning (sharding): Split table into subtables, stored in different nodes

How to do horizontal partitioning?
- Need a **partition key** (shard key): typically the **column** most frequently queried => allows for **partition pruning**, or ignore data from partions not relevant to queries.
- May run into problem where many rows go to same node unevenly
	- Low cardinality: column has few values
	- High frequency: columns has too many duplicated values
	- Can be mitigated using composite keys

How to split partition keys?
- **Range partition**: Split partition keys based on range => may lead to imbalance shards/partition
- **Hash partition**: Hash keys then partition by range => automatically spread out partition key values.

How to reduce the load when removing/adding nodes? **Consistent Hashing**.
- Tuples are assigned to the nearest node in clockwise direction.
- Adding/removing nodes only requires reassigning the tuples that come before those nodes.
- Allow a simple replication strategy: replicate a tuple in the next few (e.g. 2) nodes clockwise after the primary node.
- Multiple markers allow more equal balancing after removing a node (not all tuples will be reassigned to the next node clockwise)

### Query Processing in NoSQL

MongoDB architecture:

![[Pasted image 20231028113535.png]]

- Routers: handle requests from application and route queries to correct shards
- Config Server: stores metadata abt which shard stores which data
- Shards: stores data, consisting of 1 primary node (main computer) and 2 secondary nodes (duplicated data)

The processing order of running a queries in MongoDB:

1. Query is issued to a router (*mongos*) instance
   
2. With help of config server, *mongos* determines which shards to query

3. Query is sent to relevant shards (partition pruning)

4. Shards run query on their data, and send results back to *mongos*

5. ​​*mongos* merges the query results and returns the merged results to the application

Replication in MongoDB:
- Writes: write to primary first, then to secondary through an "operation log"
- Reads: usually read from secondary machine
	- higher throughput (physically nearer to users)
	- potentially stale data (eventual consistency)
- Elections: primary down, promote one secondary to primary








