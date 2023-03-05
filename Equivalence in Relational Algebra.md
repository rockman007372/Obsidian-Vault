## Equivalence

Motivation: Different query trees can produce the same relational output.

> [!definition]
> Expressions Q1 and Q2 are:
> - **Strongly** equivalent if they both produce error **or** both produce the same result.
> - **Weakly** equivalent **if** there is no error **then** they both produce the same result.

![[Pasted image 20230123171823.png]]

![[Pasted image 20230123171842.png]]

Observation:
- In weak equivalence, almost everything is equivalent except for non-commutativity of Cross Product and Join
- Anything with an 'if' will be equivalent in weak equivalence.