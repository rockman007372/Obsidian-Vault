Check [[Course Schedule]] and [[Alien Dictionary]] for implementation.

## Post-Order Depth First Search 

- Time and space: O(V + E)
- Process each node after it is last visited
- Add to the end of topo order

![[Topological Sort 2022-06-25 23.21.30.excalidraw]]

## Kahn's Algorithm 

- Time and space: O(V + E)
- Algorithm:

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

- If number of edges removed != |E| => There is a **cycle**!