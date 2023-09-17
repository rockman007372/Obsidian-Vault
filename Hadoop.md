![[Pasted image 20230908172559.png]]

Hadoop is a **distributed file system** designed to handle big data applications that involve **storing and processing massive volumes of data** across a distributed network of computers.

Motivation:
- Traditional architecture involves clusters of computers to do computation and clusters of storage nodes to store data. The read/write operations and tranfer of data between clusters are very costly.
- Hence, instead of moving data to worker, we move the worker to where the data is located!
	- Store data on the local disks of nodes in the cluster.
	- Start up workers on the node that has the data.

