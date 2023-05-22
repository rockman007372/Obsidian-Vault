---
tags: 
aliases: bfs
date: 2022-07-24 Sunday
---

# CS2040S

## Algorithm
1. Start at the root node
2. Visit its adjacent nodes, add them to current frontier, skip visited nodes
3. Repeat for each frontier

![[Breadth First Search 2022-06-21 17.05.49.excalidraw]]

## Implementation
Using a Queue/Linked List as frontiers

![[Breadth First Search 2022-06-21 17.04.08.excalidraw]]

## Properties
1. Parent edges form a tree (**no cycle**)
2. Parent edges form the **shortest path** from root
    + [[SSSP]] for unweighted/equally-weighted graph
    + Shortest path always forms a tree assuming there is a unique shortest path
3. Fail to visit every node if graph has multiple connected component (disjointed graphs)
	+ Must explicitly check if every node is visited, else run BFS on that node
4. Runtime for 
	+ Adjacency List: O(V + E)
	+ Adjacency Matrix: O($V^2$)

**Note**
- Do not use BFS, DFS to explore all possible paths
	- This can run to exponential time O($2^n$)
	- Does not work because we don't revisit visited nodes anw
	- ![[Breadth First Search 2022-06-21 17.46.01.excalidraw]]


# CS2109S

**Search Strategy:** Expand **shallowest unexpanded** nodes. 

**Implementation:**  frontier is a **FIFO queue**

**Properties:**

- Complete: **YES** if b is finite 
- Time: $1 + b + b^2 + b^{3} + \cdot\cdot\cdot + b^{d} + b(b^{d}-1)= O(b ^ {d + 1})$ 
	- d is the depth of the shallowest goal node
	- This is basically the number of nodes: O(N)
	- ![[Problem-Solving Agents in AI 2022-08-20 12.50.29.excalidraw]]
- Space: $O(b ^ {d + 1})$ 
	- In worst case, every node *at depth d + 1* of the search tree are in the fringe/frontier
	- ! **Dependent on when goal checking is done** → If goal test is done before pushing nodes to queue, space is **reduced** to $O(b^d)$, because we do **not** have to store and check the **last level**
- Optimal:
	- **Yes** (*only if step cost is identical, VERY IMPORTANT*), as cost only increases as we go deeper, and we only go deeper if the previous depth did not yield goal node
	- Else, path to the shallower goal states which we must first visit can be higher than the deeper goal state

>[!Important]
> **Space is a bigger problem than time** → Hence we need Iterative Deepening Search to solve space!

