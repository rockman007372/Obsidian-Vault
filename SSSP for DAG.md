---
tags: DAG, SSSP
---

Key idea: We can quickly find [[SSSP]] in a [[Directed Acylic Graph|DAG]] by relaxing every edge in topological order.

>[!algorithm]
>1. Find topological order using [[Algorithms to find topological order | topo sort algorithms]] → O(V + E)
>2. Relax the edges in this order of nodes -> O(E)

Negative edges are allowed, because in a DAG, there cannot be any negative weight cycle.

##### Special cases
- We can find Longest Path in a DAG by negating the edges and find SSSP by relaxing in order, since there will never be cycles.
- Cannot do the same trick for general (directed) graph (NP-hard) due to cycles.
