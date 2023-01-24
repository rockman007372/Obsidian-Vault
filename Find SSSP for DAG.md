---
tags: DAG, SSSP
---
Date:: 2022-08-03 Wednesday
Tags: [[SSSP]] - [[Directed Acylic Graph]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# DAG SSSP

##### Overview
- We can quickly find SSSP in DAG by relaxing every edge in topological order.
- Algorithm:
>1. Find topological order using Kahns' Algo or PostOder DFS (see [[Topological Sort]]) → O(V + E)
>2. Relax the edges in this order -> O(E)
- Negative edges are allowed, because in a DAG, there cannot be any negative weight cycle.

##### Special cases
- We can find Longest Path in a DAG by negating the edges and find SSSP!
- Cannot do the same trick for general (directed) graph (NP-hard) due to cycles.
