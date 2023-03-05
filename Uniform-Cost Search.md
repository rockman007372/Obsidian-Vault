## Strategy
Expand unexpanded nodes with **lowest path-cost** `g(n)`

## Imprementation
Frontier = [[Priority Queue]] ordered by path cost `g`.

## Comparison with other search strategies

**Equivalent to BFS if step costs are all equal**, else it is a **variant** of  [[Dijkstra's Algorithm]]

**Difference** from Dijkstra: 
We check whether a node is a goal state (**goal check**) after we pop it from PQ. In Dijkstra, we do not do goal check anywhere (It's simply a SSSP algorithm).

## Properties

- Complete: **yes**, if step cost ≥ ε > 0
	- Assuming that the branching-factor _b_ is finite, and that the step costs are >= ϵ where ϵ is some small positive-number. 
	- If the second assumption does not hold, it can get stuck in an infinite loop if there is a path with an infinite sequence of zero-cost actions (i.e., a sequence of **NoOp** actions - **only in tree search**). Completeness is therefore guaranteed provided the cost of every step exceeds some small positive-constant ϵ.
	- Negative edge cost can result in a negative weight cycle.
- Time:
	- ![[Problem-Solving Agents in AI 2022-08-20 16.25.55.excalidraw|300]]
	- b is the branching factor and C* is the total cost of the optimal solution
	- Why: Every action costs at least ϵ, so there are a total of $C^{*} / ϵ$ steps (level) to reach the goal state. *Every time we reach a node, we expand at most b nodes*. Just like BFS, in the worst case we also have to check every node. Total = 1 + b + b^2 + ... + b^(C/ε) 
- Space: Same - $O(b^\frac{C*}{ε})$, max number of nodes in the PQ at the last level (frontier)
- Optimal: **Yes**, node expanding in *increasing orders of g(n)*
	- Basically, when a node `n` is selected for expansion, the optimal path to that node has been found (Greedy algorithm)
	- Why? Assume `n` is expaned, yet there exists another frontier node `n'` on the optimal path from the start node to `n`. By definition, `n'` would have a lower `g`-cost than `n` and would have been selected first. Since step-costs are non-negative, paths will never get shorter as nodes are added.