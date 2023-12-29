---
tags: []
course: CS3230
type: lecture
date: 2023-10-29 Sunday
---

A flow network:
- Source s and Sink t
- Directed edges with capacity c

## s-t Cut

>[!definition]
>An s-t cut is a partition of nodes into 2 parts (A, B) where s $\in$ A and t $\in$ B.

Remember that {s} alone is also a valid partition.

**Capacity** of a cut : 

$$cap(A, B) = \sum_{\text{e out of A}}c(e)$$

![[Pasted image 20231029213944.png]]

>[!goal]
>We want to find the minimum cut (outgoing capacity) among all s-t cuts.

## Flow

Flow is a function f: e → f(e) such that these  2 constraints are met:
- **Capacity**: $0 \leq f(e) \leq c(e)$
- **Conservation**: $\sum(f_{in}) = \sum\limits(f_{out})$ for every node

The **value** of a flow is 

$$v(f) = \sum_{\text{e out of s}}{f(e)}$$

>[!Goal]
> Find maximum flow value possible while respecting all flow constraints.

#### Flow value lemma
Let f be any flow and (A, B) be any s-t cut. Then 

$$\sum{f_\text{out of A}} - \sum{f_\text{into A} = v(f)}$$
- Equivalent idea: water directed into s can only circulate inside the flow network in constant amount.

#### Weak duality
The value of any flow is at most the capacity of any cut.

>[!Corollary]
> If v(f) = cap(A, B), then **f is the max flow** and **(A, B) is the min cut.**

This means to find max flow, we can find min cut instead!

## Ford-Fulkerson Algorithm

Big idea is we maintain a residual graph which contains the flows we can "undo", such that by undoing these flows we can achieve a max flow.

Initially, the algorithm starts by setting the flow value between the source and sink node to 0. **At each iteration, we find an augmented path and increase the flow value.** We’ll terminate the algorithm and return the flow value when no more augmented paths can be found.

```
maxFlow(G, s, t, c):
	for each e in E:
		f(e) = 0
	Gf <- G // initially, residual graph is identical to G
	
	while (there exists an augmenting path P in Gf):
		f <- augment(f, P)
		Gf <- update(Gf)
		
	return f	
```

Theorems:

1. **Augmenting path theorem:** Flow f is max flow ⇔ there are no more augmenting paths.
2. **Max-flow min-cut theorem:** max flow = min cut
3. **Integrality theorem:** If all capacities are integers, there exists a max flow where every flow value is an integer.

Assumptions: 
- all capacities are integer between $[1, C]$

Invariant: 
- Every flow value $f(e)$ and residual capacity $c_f(e)$ remain integers throughout the algorithm.
- The algorithm terminates in at most $v(f*) \leq nC$ iterations.
	- Pf. In the worst case, s is connected to O(n) nodes, and each iteration increases flow value by 1
- If C = 1, algo runs in O(MN) time.
	- O(M) to do bfs to find aumenting path for O(N) iterations

Runtime:
- Generic version is not polynomial?
- Capacity-scaling: O(M^2 logC)


>[!Important]
> We can find the min s-t cut from the residual graph! A is the set of nodes reachable from s in $G_f$ and B is the remaining nodes.


## Application

### Bipartite Matching

#### Matching 

>[!Definition]
> A subset of the edges E is a matching if each vertex appears in at most one edge of that matching.

![[Pasted image 20231029224220.png]]

#### Problem statement

Given a bipartite graph, we want to find the maximum cardinality matching (max number of edges from one partition to the other s.t **each edge cannot share a vertex**).

![[Pasted image 20231029224902.png]]

Solution: 
- model the problem as a max-flow, min-cut problem!
- max flow v(f) = max cardinality of the matching.
- **"each edge cannot share a vertex"** ⇒ flow value of outgoing edges from S and incoming edges to T is 1.

![[Pasted image 20231029225100.png]]
### Perfect Matching

A matching M $\subseteq$ E is perfect if each node appears in exactly one edge in M.

- Not all bipartite graphs have a perfect matching
- Minimally, |L| = |R| ⇒ necessary condition for perfect matching

**Marriage Theorem:**
- Let G = (L $\cup$ R, E) be a bipartite graph with |L| = |R|. 
- Let S be a subset of nodes, and let N(S) be the set of nodes adjacent to nodes in S
- ! G has a perfect matching ⇔ |S| $\leq$ |N(S)|  for all subsets S $\subseteq$ L