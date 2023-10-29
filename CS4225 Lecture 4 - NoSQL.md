---
tags: []
course: CS4225
type: lecture
date: 2023-09-23 Saturday
---

What is NoSQL? 
- Stands for Not Only SQL.
- Non-relational databases (on top of traditional relation-based)

Types of NoSQL:
- [[Key-Value Stores]]
- [[Document Stores]]
- [[Wide Column Stores]]
- [[Graph Database]]
- [[Vector Database]]

Characteristics:
1. Horizontally scalable: can distribute data accross many machines
2. Replicate data over many servers
3. Simple call interface
4. Weaker concurrency model than RDBMS 
5. Efficient use of distributed indexes and RAM
6. Flexible schemas

Pros:
- Flexible schema
- Horizontal scalable
- High performance and availability

Cons:
- Weaker consistency guarantees.
- No declarative query language, needs to be coded on application side.

>[!factors to choose appropriate DBMS]
> - Complexity of queries
> - Importance of consistency
> - Importance of availibility and performance
> - Storage scalability

Key concepts:
- [[Strong vs Eventual Consistency]]
- [[Duplication]]



