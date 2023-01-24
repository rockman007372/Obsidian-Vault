---
tags: processed
course: CS2109S
type: lecture
date: 2022-09-06 Tuesday
---
Links: [[CS2109S]]
- - -

## Notes

We apply Adversarial Search in [[Zero-sum Games]], where one player win at the expense of the other's loss.

Some characteristics of the games we consider:
 - Deterministic: Outcome is decided deterministically by functions
 - Discrete states and decisions
 - Finite number of states and decisions
 - Perfect information
 - Zero-sum

What makes these games difficult?
 - Search space is too large (too many nodes)
 - Cannot find optimal decision
 - Time limits

Formal definition of a game:
 - S → Finite set of states (Include info on which player turn to move)
 - I → Initial board position and whose turn to move first
 - Successor() → Take current state and returns a list of (move, state) pairs.
 - T → Terminal test which determine when the game ends. 
 - U → Utility function, map terminal states to real number.

2 adversarial searches:
- [[Minimax Search]]
- [[α-β Pruning]]

### Minimax Search
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

### α-β Pruning
We can cut Minimax time complexity in half by **pruning**. The idea is that we can compute the correct minimax decision **without looking at every node in the game tree**.

The general principle is this: 
- Consider a node _n_ somewhere in the tree, such that the player has a chance of moving to that node. 
- If the player has a better choice _m_ either at the parent of node _n_, or at any choice point further up, then _n_ will never be reached in actual play. 
- So once we have found out enough about _n_ (by examining some of its descendants) to reach this conclusion, we can prune it.

The algorithm gets its name from the following two parameters that describe the bounds on the backed-up values that appear anywhere along the path:
-   **α** = best (largest) value for **MAX** so far on current path.  
-   **β** = best (smallest) value for **MIN** so far on current path.
-   If at a MIN node, prune if minimax value of node $\le \alpha$
-   If at a MAX node, prune if minimax value of node $\ge \beta$
-   Basically, whenever $\alpha \geq \beta$ → prune!!!

![[Adversarial Search 2022-09-07 21.53.26.excalidraw]]

Pseudo-Code:
```java
function ALPHA-BETA-SEARCH(state) returns an action 
	inputs: state, current state in game 
	v ← MAX-VALUE(state, -∞, +∞) 
	return the action in SUCCESSORS(state) with value v

function MAX-VALUE(state, a, b) returns a utility value 
	inputs: state, current state in game 
			alpha, best MAX value along the path to state
			beta, best MIN value along the path to state
	
	if TERMINAL-TEST(state) then return UTILITY(state) 
	
	v ← -∞ 
	for a, s in SUCCESSORS(state) do: 
		v ← MAX(v, MIN-VALUE(s, a, b)) 
		if v ≥ b then return v # compare to b 
		a ← MAX(a, v) return v # update a
	return v

function MIN-VALUE(state, a, b) returns a utility value 
	inputs: state, current state in game 
			alpha, best MAX value along the path to state
			beta, best MIN value along the path to state
	
	if TERMINAL-TEST(state) then return UTILITY(state) 
	
	v ← +∞ 
	for a, s in SUCCESSORS(state) do: 
		v ← MIN(v, MAX-VALUE(s, a, b)) 
		if v ≤ a then return v # compare to a 
		b ← MIN(b, v) return v # update b
	return v
```


In the best case, Alpha-Beta reduces complexity by **half** (prune one of the highest children?) → Time Complexity = $O(b ^{m/2})$ → It can search about **twice as far** (deep) as minimax in the same amount of time.

Order of search matters in terms of performance but not completeness. This means a different order of search can take a longer time (due to fewer pruning), but always return the same path (result).

### Cutting-off Search
The search space can be very large, and we may not be able to reach the terminal leave. In such case, we can have a **cutoff limit** combined with an **evaluation function** to limit the depth of our search.

It is identical to Minimax, except:
- `isTerminal()` is replaced by `isCutoff()`
- `Utility` is replaced by `Evaluation`

The evaluation function estimates the *expected utility* of a state of the game (the state does not have to be terminal state!). 

## Negamax 

The same idea as minimax, but instead of having one maximizer and one minimizer, both are maximizing their own score where their score is the negation of one another.

![[Enhanced-NegaMax-with-Alpha-Beta-Property-Pseudo-Code.png]]

## Summary

## Questions/Cues

