---
tags: DataStructure, SSSP
---
Date:: 2022-08-03 Wednesday
Tags: [[SSSP]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

###### Use:
- Find the shortest distance between 2 nodes
- Find the shortest distance between a source and every other node
- Detect negative weight cycles

###### Triangle Inequality
>$D(S, C) <= D(S, A) + D(A, C)$

![[Bellman-Ford SSSP 2022-08-03 13.35.40.excalidraw||500]]

###### Algorithm
![[Pasted image 20220803133410.png]]
![[Pasted image 20220803141631.png]]

- Initially, assign the estimates of every node to Infinity.
- Let the estimate of the source be 0.
- Relax every edge of the graph in random order.
	- Relax function: to update the current estimate (minimum distance) of a node to the source, by making used of Triangle Inequality.
```Java
relax(int u, int v) {
	if (dist[v] > dist[u] + weight(u, v))
		dist[v] = dist[u] + weight(u, v);
}
```

- Since the correct estimate can only be found by relaxing every edge in the correct order (In Breadth First Search order away from the source), we must relax for V - 1 iterations.
```
n = V.length;
for (i = 0; i < n - 1; i++) {
	for (Edge e : graph) {
		relax(e)
	}
}
```

- We can terminate early if one iteration does not change any estimates.
- Runtime: O(EV)

###### Why must we iterate V - 1 times?
![[Pasted image 20220803142438.png]]
- After 1 iteration, the node on the shortest path that is one hop away has the correct estimate.
- After 2 iterations, the node on the shortest path that is 2 hop away has the correct estimate (by building on the previous 1-hop node)
- Key property: If P is the shortest path from S to D, and X is on path P, then P is also the shortest path from S to X.
- Hence we have the invariant:
> After n iterations, the n<sup>th</sup> node from the source on the SHORTEST PATH TREE has the correct estimate. 

- Another way to look at it:
>After n iterations, all the node AT MOST n hops away from the source have the correct estimate.
>![[Pasted image 20220803142317.png]]

- This does not mean EVERY node n-hop away from source has correct estimate at n iteration! (Dependent on order of relax) 

###### Special cases
- Bellman-Ford works with negative weight edges. However, we cannot find SSSP if there is negative weight cycle (as estimate will keep decreasing after every iteration) → Bellman-Ford can detect negative weight cycle by checking if estimates still change after V iterations.
- For unweighted graphs, just use [[Breadth First Search]].