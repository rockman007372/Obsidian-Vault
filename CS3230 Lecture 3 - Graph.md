---
tags:
  - toProcess
course: CS3230
type: lecture
date: 2023-08-29 Tuesday
---

- What are graphs?
- Graph representation:
	- Adjacency Matrix: 
		- for dense matrix w lot of edges
		- 2 representation of each edge
		- check if (u, v) is an edge takes O(1) time
		- Identify all edges takes O(n^2)
		- space = O(n^2)
	- Adjacency List: Each node has a list of neighbors
		- for sparser graphs like trees with fewer edges
		- space = O(m + n), where m is # nodes and n is # edges
		- check (u, v) takes O(deg(u))
		- identify all edges takes O(m + n)
		- why m + n? check each node once and **each edge at most twice**
- paths and connectivity
	- a path is a sequence of consecutive nodes connected by edges
	- a simple path: no repeated nodes (all **distinct** nodes)
	- graph is connected = there is a path btw every 2 nodes
- cycle: same start and end node, else no repeated nodes
- tree: **connected** undirected graph with **no cycle**
	- ! Tree theorem: Let G be an undirected graph on n nodes. Any 2 of the statements imply the third:
		- G is connected
		- G does not contain a cycle
		- G has n - 1 edges
- rooted tree
- [[Breadth First Search]]
	- Property: the level of x and y differ by at most 1 where (x, y) is an edge of G
	- BFS forms a tree
	- runtime: O(m + n) if graph is adj list. 
- Connected components
	- flood filling problem
	- can be solved using bfs

>[!question]
> Let G be a graph on n nodes where n is even. Suppose every node in the graph has degree at least n/2. Then G is connected. True or false? Why?

> [!Answer]
> - Yes
> - Assumes G is not connected, there are at least 2 separated components c1 and c2
> - Every node has degree of at least n/2, hence a node in c1 is connected to at least n/2 other nodes. Hence there are at least n/2 + 1 nodes in c1
> - Similary there are at least n/2 + 1 nodes in c2
> - In total, there are at least n + 2 nodes, which contradicts G having n nodes.

- [[Bipartite Graph]]: every edge has one red and one blue end
	- not obvious from drawing!
	- given a graph G, is it bipartite?
	- ! lemma 1: if G is bipartite, it cannot contain odd length cycle
	- ! lemma 2:  BFS layers vs bipartite graph
	- Corollary: G is bipartite **iff** it contains no odd length cycle => this is the **only obstruction to a graph being bipartite or not.**
- Directed graph
	- Strong connectivity in directed graph: if there is a path **from u to v** and a path from **v to u** (mutually reachable)
	- ! lemma: let s be any node. G is strongly connected iff **s is mutually reachable to every other node**
		- Just have to look at one node to prove strong connectivity.
		- Reduce time to check to O(m + n)!!!! 
			- run bfs from s in G: check if s is connected to every node
			- ! run bfs from s in G_reverse: check if every node is connected to s
- Directed Acylic Graph: directed graph with no cycle
	- [[Topological Order]]
	- lemma: If G has a topological order, then G is a DAG
	- lemma: If G is a DAG, then G has a node with no incoming edges (source node)
	- lemma: If G is a DAG, then G has a topological order (by an algo based on the above lemma)
	- [[Algorithms to find topological order]] all takes O(m + n) time