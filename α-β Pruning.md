We can cut Minimax time complexity in half by **pruning**. The idea is that we can compute the correct minimax decision **without looking at every node in the game tree**.

The general principle is this: 
- Consider a node _n_ somewhere in the tree, such that the player has a chance of moving to that node. 
- If the player has a better choice _m_ either at the parent of node _n_, or **at any choice point further up**, then _n_ will never be reached in actual play. 
- So once we have found out enough about _n_ (by examining some of its descendants) to reach this conclusion, we can prune it.

The algorithm gets its name from the following two parameters that describe the bounds on the backed-up values that appear anywhere along the path:
- **α** = best (largest) value for **MAX** so far on current path.  
- **β** = best (smallest) value for **MIN** so far on current path.
- Initially, **α** = - inf and **β** = + inf
- Update **α** at MAX node and **β** at MIN node.
- At a MIN node, prune if minimax value of node $\le \alpha$
- At a MAX node, prune if minimax value of node $\ge \beta$
- Basically, whenever $\alpha \geq \beta$ → prune the node and stops checking its remaining children. 

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


Time Complexity = $O(b ^{m/2})$ 
- It can search about **twice as far** (deep) as minimax in the same amount of time.
- Why? Something to do with skipping every other level in the best case when the pruning order is optimal.

Order of search matters in terms of performance but not completeness. This means a different order of search can take a longer time (due to fewer pruning), but always return the same path (result).

### Cutting-off Search

The search space can be very large, and we may not be able to reach the terminal leaves. In such case, we can have a **cutoff limit** combined with an **evaluation function** to limit the depth of our search.

It is identical to Minimax, except:
- `isTerminal()` is replaced by `isCutoff()`
- `Utility` is replaced by `Evaluation`

The evaluation function estimates the *expected utility* of a state of the game (the state does not have to be terminal state!). 