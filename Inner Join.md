
- Includes only tuples that satisfy the condition.
- Consists of:
	- $\theta$-Join $\Join_{theta}$
	- Equi-Join $\Join_{=}$
	- Natural Join $\Join$

## Theta Join 

$$R \Join_{theta} S = \sigma_{[\theta]}(R \times S)$$

> [!example]
> For all the projects, find the offices of the managers.

$$Projects ⋈[manager=mname]
(ρ[mname←name](Managers))$$
## Equi Join

$$R \Join_{=}S$$
- A special θ-join where the only relational operator that can be used is equality (e.g., = or ≡)
- Can use arbitrary relational operator (=, <, >, <>, ...)
- ? Most common Inner Join operation, especially when performing inner join following foreign key constraints

Example: 

```yaml
orders table:
order_id | customer_id | order_date | total_amount
1        | 101         | 2022-01-01 | 100.00
2        | 102         | 2022-01-02 | 50.00
3        | 101         | 2022-01-03 | 75.00
4        | 103         | 2022-01-04 | 200.00

customers table:
customer_id | customer_name
101         | John Smith
102         | Jane Doe
103         | Bob Johnson

```

```sql
SELECT *
FROM orders JOIN customers
	ON orders.customer_id = customers.customer_id;
```

## Natural Join

$$ R \Join S = \pi_{[l]}(R \Join_{[\theta]}S)$$
where:
- $l = Attr(R) \cup (Attr(S) - Attr(R)) =  Attr(R) \cup Attr(S)$
- $\theta = \forall A_{i} \in Attr(R) \cap Attr(S): R.A_{i}= S.A_i$

**In other words,** The join is performed over all **common attributes** btw R and S such that:
- We only combine if the value of the common attributes are equals
- ! The output relations contains the common attribute of R and S **only once**.

>[!note]
> - If there are non-matching values of **any** of the multiple common attributes in either table, those values will not be included in the natural join result.
> - If there is no common attribute, natural join is reduced to **cross product**, not empty table

**Example**
Find the office of the manager in charge of each project.

![[Pasted image 20230123171133.png]]

- We rename attribute `Managers.name` to `Managers.manager` to match the name of the attribute `Project.manager`
- Natural join will check the the common attribute `manager` and perform cross product only if the attribute values are the same (eg. `manager == Judy`)

