---
tags: processed
course: CS2109S
type: lecture
date: 2022-09-06 Tuesday
---
Links: [[CS2109S]]
- - -


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

Formal definition of a game: SISTU

 - S → Finite set of states (Include info on which player turn to move)
 - I → Initial board position and whose turn to move first
 - Successor() → Take current state and returns a list of (move, state) pairs.
 - T → Terminal test which determine when the game ends. 
 - U → Utility function, map terminal states to real number.

Type of adversarial searches:

- [[Minimax Search]]
- [[α-β Pruning]]
- [[Negamax]]


