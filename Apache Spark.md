Apache Spark is an open-source, distributed computing system used for big data processing and analytics.

Motivation:
- **Speed:** Stores intermediate results in RAM, not disk => suitable for **iterative algorithms** / **interactive data analysis** (less disk I/O).
- **Ease of Use:** Spark offers high-level APIs for various programming languages including Scala, Java, Python, and R.
- **Distributed Processing:** Spark distributes data across a cluster of machines, allowing **parallel processing**.
- **Flexibility:** Spark can read data from various data sources like [[HDFS]]
- **Fault Tolerance:** rebuild lost data due to node failures by using **lineage information** to recompute only the lost data partitions instead of re-running the entire job.

## Component and API stacks

![[Pasted image 20231028145528.png]]