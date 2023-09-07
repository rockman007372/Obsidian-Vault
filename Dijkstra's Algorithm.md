---
tags: DataStructure, SSSP, Greedy
date: 2022-08-03 Wednesday
---
Tags: [[SSSP]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

## Overview

A greedy SSSP algorithm in which we only relax each edge once (by following the "right" relax order).

Idea:
- Keep a set of visited nodes
- Relax the shortest edge between the set and the unvisited nodes
- The vertex with the smallest estimate is extracted using [[Priority Queue]]

![[Dijkstra's Algorithm 2022-08-03 22.07.13.excalidraw]]

## Algorithm

1. Initialize distance estimate of every node to Infinity
2. Initializing source's estimate to 0
3. Create set S of visisted nodes and a Priority Queue PQ to store unvisited nodes.
4. While (PQ is not empty)
	1. ExtractMin from PQ to get node with min estimate
	2. Add this node to S
	3. Relax all outgoing edges, add and update estimate in PQ

## Illustration

![[Pasted image 20220803222204.png]]
![[Pasted image 20220803222221.png]]
![[Pasted image 20220803222247.png]]

## Pseudo Code

```Java
public Dijkstra {
	private Graph G;
	private PriorityQueue pq = new PriorityQueue();
	int[] estimates;
	
	searchPath(int start) {
		estimates = new int[G.size()];
		Arrays.fill(estimate, Infinity);
		pq.insert(start, 0);
		while (!pq.isEmpty()) {
			int w = pq.deleteMin(); // node with min estimate
			for (Edge e : G[w].neighbors) {
				relax(e); // relax all outgoing edges of w
			}
		}
	}
	
	relax(Edge e) {
		int v = e.from();
		int w = e.to();
		int weight = e.weight();
		// only update if a shorter estimate is found
		if (estimates[w] > estimates[v] + weight) {
			estimates[w] = estimates[v] + weight;
			parent[w] = v; // update shortest path tree
			
			// update PQ with new estimates
			if (pq.contains(w)) {
				pq.decreaseKey(w, estimates[w]);
			} else {
				pq.insert(w, estimates[w]);
			}
		}
	}
}
```

##### Time Complexity
- Each node is extracted from PQ once -> O(V * lgV)
- Each edge is relaxed once, and each relax call costs O(lgV) -> O(E * lgV)
- Total: O((E + V) * logV) = O(ElogV) since E = O(V)

## Why does it work

- **Whenever we extract a node from the PQ, the node has the correct estimate (the shortest distance from the source).**
- Because all edges are positively weighted, extending a path will only make it longer.

![[Dijkstra's Algorithm 2022-08-03 22.35.13.excalidraw]]

- Dijkstra's stops working if edges are negative, because extending a path can make it shorter (hence a node may be updated later after it has been extracted from PQ, hence not greedy anymore).

## Comparison 

- [[Breadth First Search]] takes edges from vertex that was discovered least recently -> Use Queue
- [[Depth First Search]] takes edges from vertex that was discoverd most recently -> Use Stack
- Dijkstra takes edges from vertex closest to source -> Use Priority Queue

