---
tags: 
aliases:
  - HDFS
date: 2023-09-08 Friday
---

>[!definition]
> HDFS stands for Hadoop Distributed File System.

HDFS is a **distributed file system** designed to handle big data applications that involve **storing and processing massive volumes of data** across a distributed network of computers.

#### Motivation

![[Pasted image 20230923112426.png]]

- Traditional file system architecture involves clusters of computers to do computation and clusters of storage nodes to store data. 
- The read/write operations and tranfer of data between clusters are very costly.

#### Solution

Instead of moving data to workers, we move the workers to where the data is located!
- Store data on the local disks of nodes in the cluster.
- Start up workers on the node that has the data.

## Design Decisions

1. Files are stored as fixed chunks.
2. Each chunk is replicated across 3+ servers (ensure reliability)
3. Single master to coordinate access through metadata.

![[Pasted image 20230908172559.png]]

