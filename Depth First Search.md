2022-06-21 17:16
Tags: [[Data Structure and Algorithm]] - [[Graph]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
# CS2040S

## Algorithm
Based on recursion:
1. Visit every adjacent node recursively still stuck
2. Backtrack to until we find an unvisited adjacent node
3. Recurse
4. Do not repeat visited nodes

![[Depth First Search 2022-06-21 17.18.13.excalidraw]]

For a rooted tree: PreOrder, InOrder, PostOrder are forms of DFS

**Why is the time complexity of depth first search algorithm O( V + E ) :** When the graph is stored in an adjacency list, the neighbors of a vertex on the out going edge are explored successively/linearly. As each vertex is explored only once, all the vertices are explored in O ( V ) time. The total number of edges (maintained in the adjacency list) are 2*E (bi-directional) for an undirected graph and E for a directed graph. Thus the time complexity is O ( 2.E + V ) for an undirected graph and O ( E + V ) for a directed graph.

## Implementations
### Recursion 
```Java
DFS(Node[] nodeList) { 
	boolean[] visited = new boolean[nodeList.length]; 
	Arrays.fill(visited, false); 
	// check every node in case there are connected components
	for (start = i; start < nodeList.length; start++) {
		if (!visited[start]) { 
			visited[start] = true; 
			DFS-visit(nodeList, visited, start); 
		}
	}
}

DFS-visit(Node[] nodeList, boolean[] visited, int startId) {
	for (Integer v : nodeList[startId].nbrList) { 
		if (!visited[v]) { 
			visited[v] = true; 
			DFS-visit(nodeList, visited, v); // recursively visit every adjacent nodes
		} 
	} 
}
```

### Stack
![[Depth First Search 2022-06-21 17.28.16.excalidraw]]

## Properties
1. DFS graph forms a tree
2. **NOT** a shortest path tree
3. Space: O(V + E) for Adj List, O($V^2$) for Adj Matrix
4. DFS can **detect cycles** in a directed graph (BUT [[Breadth First Search]] CANNOT)
	+ To detect a back edge, keep track of vertices **currently in the recursion stack** of function for DFS traversal. If a vertex is reached that is already in the recursion stack, then there is a cycle in the tree.
	+ ![[Depth First Search 2022-06-21 17.42.30.excalidraw]]



# CS2109S

- Expand **deepest unexpanded** nodes
- Implementation: Frontier = **stack**

Properties:
- Complete: **No**
	- **WHY:** fail in infinite-depth spaces and spaces with loops → Must limit the depth + avoid repeating states along the path 
	- Complete in finite space
- Time: $O(b^m)$ = $1 + b + b^2 + ... + b ^{m}$ 
	- Terrible if m (max depth) is much larger than d (least depth)
	- If solutions are dense yet depth is low, may be much better than BFS (*EG: RUBIK CUBE SOLVING*)
	- Equals O(N) where N is no. nodes
- Space: O(b * m) - linear space, very space efficient
	- **Why:** m = the length of the longest path. For each node, you have to store all b siblings so that you know which sibling to explore next after completing a branch → for m nodes down the path, must store its b sibling per node. 
- Optimal: **NO**
	- **WHY:**  Even when step costs are equal, DFS is still non-optimal, because the deepest goal node may be reached first and incurs greater cost.
	- ![[Problem-Solving Agents in AI 2022-08-27 18.30.06.excalidraw||300]]