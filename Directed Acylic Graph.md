---
tags: [graph, DataStructure]
aliases: [DAG, dag]
---
Date:: 2022-08-03 Wednesday
Tags: [[Graph]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

### Main Points
- A DAG is a directed graph with no cyclic dependencies (no cycle).
- All DAG has a topological order (See [[Topological Sort]])
- For DAG, we can find SSSP more quickly by relaxing the edges in topological order. See [[Find SSSP for DAG]]