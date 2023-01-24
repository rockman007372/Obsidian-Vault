2022-06-21 15:41
Tags: [[Data Structure and Algorithm]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# Graph
### Key Points
##### Graph definition
A graph consists of 
1. Nodes (>= 1) 
   => V = set of nodes
2. Edges connecting 2 nodes 
   => E = set of edges = { (u, v) : u, v $\in$ V }

##### Path 
![[Graph 2022-06-21 15.50.30.excalidraw|300]]

##### Connected vs Disconnected Components
![[Drawing 2022-06-21 15.52.10.excalidraw|300]]

##### Cycle
There is a path starting from one vertex to the same vertex without repeating any edges

##### Tree
*Connected* graph with *no cycle*.
Theorem: A graph has V = N, E = N - 1 and is connected $\Leftrightarrow$  graph is a tree.

##### Forest
Graph with no cycle (can be disconnected)

##### Degree
1. Node: number of outgoing/incoming edges in that node
   
   ![[Graph 2022-06-21 16.02.48.excalidraw|200]]
2. Graph: **Max** number of adjacent edges
   
   ![[Graph 2022-06-21 16.04.15.excalidraw|200]]

##### Diameter
Max distance between 2 nodes in the graph, following the ***shortest path***. (the length of the longest chain you are forced to use to get from one vertex to another in that graph)

You can find the diameter of a graph by finding the distance between every pair of vertices and taking the maximum of those distances.

![[Graph 2022-06-21 16.13.37.excalidraw]]

##### Special Graphs
###### Stars 
E = N - 1
Diameter = 2

![[Graph 2022-06-21 16.16.09.excalidraw|200]]

###### Complete Graph / Clique
|E| = $n \choose 2$= $\frac{(n)(n-1)}{2}$ = O($V^2$)   
Diameter = 1
Degree = n - 1

![[Graph 2022-06-21 16.22.10.excalidraw|200]]

###### Line 
Diameter = n - 1
Degree = n
|E| = n - 1

![[Graph 2022-06-21 16.27.06.excalidraw]]

###### Cycle
Diameter = $\frac{n}{2}$ if n is even, $\lfloor \frac{n}{2} \rfloor$  if n is odd
Degree = 2

![[Graph 2022-06-21 16.35.49.excalidraw|300]]

###### Bipartite Graph
Diameter <= n - 1
degree = 2

![[Graph 2022-06-21 16.39.44.excalidraw]]

A graph is bipartite if the vertices can be divided into 2 disjointed and independent set U and V, where every edge connects a vertex in U to one in V.

##### Graph Representation
###### Adjacency List
![[Graph 2022-06-21 16.48.38.excalidraw|300]]
- Can be undirected or directed
- Space complexity: O(V + E)
- For Cycle: O(V) since E = V - 1
- For Clique: O($V ^ 2$) since E = O($V^2$)
  
######   Adjacency Matrix
![[Graph 2022-06-21 16.51.02.excalidraw|300]]

- Space: O($V^2$) for everything

###### Base Rule
If graph is dense, use Adjacency Matrix. Else, use Adjacency List.
Dense: |E| = O($V^2$)

###### Trade-offs
| Adjacency List                      | Adjacency Matrix |
| ----------------------------------- | ---------------- |
| Fast Query: Find me any neighbor    | Slow Query: Find me any neighbor of v    |
| Fast Query: Enumerate all neighbors | Slow Query: Enumerate all neighbors of v |
| Slow Query: Are u and v neighbors   | Fast Query: Are u and v neighbors        |


