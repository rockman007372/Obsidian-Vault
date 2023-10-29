## Motivation

>[!question]
> Find the name of a restaurant that sells all pizzas liked by 'Homer'

## Problem
- SQL queries evaluate each row one-by-one.
- But in the example above, we need to evaluate multiple rows (to ensure all the pizzas sold by the restaurant are liked by Homer).

## Solution 1: **Double negation**

Restaurants that sell **all** pizzas liked by 'Homer'
= There exists **no** pizzas that Homer like **and** the restaurant does not sell them.

In discrete math terms: $\forall = \neg(\neg\exists)$
$$
\begin{align*}

\forall x \in \text{Homer's pizza}: Sell(x) \\
\iff \neg \neg (\forall x: Sell(x)) \\
\iff \neg (\exists x : \neg Sell(x)) 

\end{align*}
$$
Query:

```sql
SELECT DISTINCT S1.rname
FROM Sells S1
WHERE NOT EXISTS (
	SELECT 1 FROM Likes L
	WHERE L.cname = 'Homer'
	-- the restaurant does not sell a pizza that Homer likes
	AND NOT EXISTS (
		SELECT 1 FROM Sells S2
		WHERE S2.pizza = L.pizza
		AND S2.rname = S1.rname
	)
);
```

## Solution 2: **Cardinality**

Let R be the pizzas sold by restaurant 'R'.
Let S be the pizzas liked by 'Homer'.

Restaurant 'R' sells **all** pizzas liked by 'Homer' 
$\iff S \subseteq R \iff S \cup R = R \iff \lvert S \cup R \rvert = \lvert R \rvert$ 

Solution:

```sql
SELECT DISTINCT rname 
FROM Sells S 
WHERE 

( 
	SELECT COUNT(DISTINCT pizza) 
	FROM ( 
		SELECT pizza FROM Sells S1 WHERE S1.rname = S.rname 
		UNION 
		SELECT pizza FROM Likes WHERE cname = 'Homer' 
	) AS T1 
) 

= 

( 
	SELECT COUNT(DISTINCT pizza) 
	FROM Sells S1 
	WHERE S1.rname = S.rname 
);

```

![[Pasted image 20230427140916.png]]



