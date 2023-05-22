---
tags: [graph, DataStructure]
aliases: [DAG, dag]
date: 2022-08-03 Wednesday
---
Tags: [[Graph]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

![[Pasted image 20230518141113.png]]

- A DAG is a directed graph with no cyclic dependencies (no cycle).
- All DAG has a [[Topological Order|topological order]].
- For DAG, we can find SSSP (single-source shorted path) more quickly by relaxing the edges in topological order. See [[SSSP for DAG]]