---
tags:
  - processed
course: CS3230
type: lecture
date: 2023-08-15 Tuesday
---

## Summary

- Stable matching
- Gale-Shapley Algorithm

## Content

>[!problem]
>Matchmaker must match n men and n women. Each man ranks all the women, and each woman ranks all the men. How to pair them up?

### Stable Matching

A matching is stable if no unmatched man **and** woman (not matched to each other) prefer each other to their current partner (have an incentive to cheat).

![[Pasted image 20230815122301.png]]


### Gale-Shapley Algorithm

```
initialize each person to be free

while (some man is free and has not proposed to all women) {
	m = such man
	w = first woman on m's list who he has not proposed
	
	if (w is free) {
		match m and w
	} else if (w prefers m to her fiance m') {
		match m and w
		set m' free
	} else {
		w rejects m
	}
}
```

>[!lemma 1]
> The while loop terminates after $\leq n^2$ times.

- A man never proposes to the same woman more than one, and he proposes all n woman in the worst case.

>[!lemma 2]
> Men propose to women in **decreasing** order of preference.

- A man m always proposes the highest-ranked woman on his list. If he becomes free in some later iterations, he must propose some woman of a lower rank.

>[!lemma 3]
> A woman stays engaged after the first time she was proposed.
> Her sequence of partner only becomes better according to her preference list.

- A woman can only change partners after shes engaged, but never becomes free
- She only changes if she finds a better partner

>[!lemma 4]
> When the algorithm terminates, each man is only engaged to a unique woman.

- Proof by contradiction: 
	- Suppose the man m is free at the end of the algorithm. This means some woman w is also not engaged.
	- However, by **lemma 3**, a woman stays engaged after the first time she was proposed. Hence w must not have been proposed to during the algorithm.
	- This contradicts the fact that m must propose to every woman **including w**.

>[!Lemma 5]
> When the algorithm terminates, the matchings btw men and women are stable.

![[Pasted image 20230815122301.png]]

- Proof by contradiction:
	- Suppose a pair (m, w) exists where m and w prefer each other to their own partners.
	- This means m is higher in preference compared to m'.
	- However, m must have proposed to w before w' because w is higher than w', and gets rejected if w is already with m', or get replaced by m' in later iterations.
	- This implies m' is higher in preference compared to m => contradiction.

##### Men-optimality 

For a man m, **best(m)** is the highest ranked woman on his list, **who could be his partner in some stable matching.**

> [!theorem]
> Gale-Shapley returns the matching in which each man m is paired with **best(m)**.

- No 2 men have the same optimal partner
- Optimizes all men's wishes simultaneously
- Order of proposal does NOT matter

##### Women-Pessimality

For a woman w, let **worst(w)** be the lowest ranked man on her list who **could be her partner in some stable matching.**

>[!theorem]
> Each woman w is paired with **worst(w)**.

## Questions/Cues

How to prove men-optimality??

---
Links:
