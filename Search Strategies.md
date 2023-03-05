
A search stategy is defined by *picking the order of node expansion* (BFS vs DFS)

Strategies are evaluated along the following dimensions:
- **Completeness**: similar to correctness, can you find the solution if theres one?
- **Time Complexity**: Number of nodes generated
- **Space Complexity**: Max number of nodes in memory (at any time)
- **Optimality**: Does it always find the least-cost solution?

Time and space are measured in terms of
- `b`: max branching factor of a search tree (from a node, what is the max number of neighbor nodes)
- `d`: depth of the *least-cost* solution (depth of the **shallowest** goal node)
- `m`: *max* depth of the state space