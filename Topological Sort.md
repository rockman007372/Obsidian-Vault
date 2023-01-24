2022-06-25 17:12
Tags: [[Data Structure and Algorithm]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
## Definitions
Topological order: Sequential total order such that all edges point forward.

If a graph has a topological order, it is a [[Directed Acylic Graph]]. A DAG is a directed graph with no cyclic dependencies (no cycle).

All DAG has a topological order.

Topological order is not unique.

![[Topological Sort 2022-06-25 23.17.53.excalidraw]]

## Algorithms to find Topological Order
Check [[Course Schedule]] for implementation.

### Post-Order Depth First Search - O(V + E)
- Process each node after it is last visited
- Add to the end of topo order
![[Topological Sort 2022-06-25 23.21.30.excalidraw]]

### Kahn's Algorithm - O(V + E)
```Java
1. S = Set of all nodes in G with no incoming edges
2. L = List of nodes in topo order
3. Add all nodes with zero incoming edges to S
4. While S is not empty:
     u = S.remove;
	 for each neighbor v of u:
	   remove edge (u, v)
	   if v has no incoming edges: add v to S
5. Repeat till S is empty
6. Return L
```

To check if there is cycle: if number of edges removed != |E|.

## Connected Component / Strongly Connected Component
Connected Component: Associated with undirected graphs
```
v & w are in a connected component
<=> there is a path from v to w
```

Strongly Connected Components: Associated with directed graph
```
v & w are in a strongly connected component
<=> there is a path from v to w && there is a path from w to v
<=> there is a ROUTE from v to w
```
![[Pasted image 20220625233502.png]]