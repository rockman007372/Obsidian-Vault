---
tags: data structure
aliases: 
date: 2023-01-14 Saturday
---

2 main ways to represent a (directed) graph:

### Adjacency List

- Array of nodes
- Each node maintains a list of neighbors
- Space: O(V + E)

![[Pasted image 20230114205948.png]]

### Adjacency Matrix
- Matrix `A[v][w]` represents edge (v, w)
- Space: O(V^2)

![[Pasted image 20230114210017.png]]

### Comparison

- Adjacency matrix allows you to quickly check if 2 nodes are neighbors. 
- Adjacency allows you to find all the neighbors of a node quickly.








---
Links: [[Data Structure and Algorithm]]
