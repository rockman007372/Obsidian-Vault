Assume there are two players MAX and MIN. MAX always chooses a move that maximizes the payoff, whereas MIN will always choose a move that will minimize MAX's payoff. 

Assume that each player plays optimally. Given a game tree, the optimal strategy can be determined from the **minimax value** of each node, which is written as `MINIMAX(n)`.

![[Pasted image 20220907165743.png]]

It operates on the assumption that players will always behave optimally. For example, MIN will always choose actions that return the lowest utility. Knowing this, MAX can choose actions that maximise his utility by forcing MIN to choose a specific paths of action. 

Minimax is a [[Depth First Search]]. It traverse all the way to the left-most terminal node, then recurse upwards.

![[Pasted image 20220907170238.png]]

Pseudo-Code:

```Java
function MINIMAX-DECISION(state) returns an action 
	inputs: state, current state in game 
	v ← MAX-VALUE(state) 
	return the action in SUCCESSORS(state) with value v 
	
function MAX-VALUE(state) returns a utility value 
	if TERMINAL-TEST(state) then return UTILITY(state) 
	v ← (-Infinity) 
	for (a, s) in SUCCESSORS(state) 
		do v ← MAX(v, MIN-VALUE(s)) 
	return v 
	
function MIN-VALUE(state) returns a utility value 
	if TERMINAL-TEST(state) then return UTILITY(state) 
	v ← Infinity 
	for (a, s) in SUCCESSORS(state) do 
		v ← MIN(v, MAX-VALUE(s))
	return v
```

Properties:
- **Completeness:** Yes if finite actions and states
- **Time Complexity:** $O(b ^ m)$ - just like DFS
- **Space Complexity:** 
	- $O(bm)$ if all successors generated at once
	- $O(m)$ if only one successor generate at a time → Recursion stack depth
- **Optimal:** Yes (against an optimal opponent)

We can also perform Minimax with 3 players:

![[Pasted image 20220907171052.png]]
