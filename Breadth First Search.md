2022-06-21 17:01
Tags: [[Data Structure and Algorithm]] - [[Graph]] - [[Depth First Search]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
### Algorithm
1. Start at the root node
2. Visit its adjacent nodes, add them to current frontier, skip visited nodes
3. Repeat for each frontier

![[Breadth First Search 2022-06-21 17.05.49.excalidraw]]

### Implementation
Using a Queue/Linked List as frontiers

![[Breadth First Search 2022-06-21 17.04.08.excalidraw]]

### Properties
1. Parent edges form a tree, *never has a cycle*
2. Parent edges form the **shortest path** from root
    + [[SSSP]] for unweighted/equally-weighted graph
    + Shortest path always forms a tree assuming there is a unique shortest path
3. Fail to visit every node if graph has multiple connected component (disjointed graphs)
	+ Must explicitly check if every node is visited, else run BFS on that node
4. Run time for 
	+ Adjacency List: O(V + E)
	+ Adjacency Matrix: O($V^2$)

### WARNING
Do not use BFS, DFS to explore all possible paths
+ This can run to exponential time O($2^n$)
+ Does not work because we don't revisit visited nodes anw
![[Breadth First Search 2022-06-21 17.46.01.excalidraw]]