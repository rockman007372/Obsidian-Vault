A graph database stores nodes and relationships instead of tables, or documents. 

Traditionally,  RDBMS store relationships through relationship tables. This requires expensive `JOIN` operations or cross-lookups, often tied to a rigid schema. It turns out that "relational" databases handle relationships poorly. 

In a graph database, there are no JOINs or lookups. Relationships are stored natively alongside the data elements (the nodes) in a much more flexible format. Everything about the system is optimized for traversing through data quickly; millions of connections per second, per core.

![[Pasted image 20230929012642.png]]