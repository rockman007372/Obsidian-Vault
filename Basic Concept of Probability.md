---
tags: processed
aliases: 
course: ST2334
type: lecture
date: 2022-08-07 Sunday
---
Course: [[ST2334]]
- - -

## Notes

### Concepts and Definitions
- Statistical experiment
- **Sample Space (S)**: set of *all possible outcomes* (All numbers on dice)
- **Sample point**: An outcome in S (a number on dice)
- **Event**: subset of sample space (event that odd number occurs)
- Sample space is itself an event and is called a **sure event**
- **Null event**: event that has no elements.
- Considering an experiment of tossing 2 dies
	- If the dies are labelled, there are 6 * 6 = 36 elements
	- If not labelled, 6 + 5 + 4 + 3 + 2 + 1 = 21 elements

### Event Operations and Relationship
- Operations:
	- **Union**
	- **Intersection**
	- **Complement**
- Relationship:
	- Contained
	- Equivalent
	- Mutually exclusive
	- Independent
- Intersection and Union can be **extended to n event**
  
### Basic Set Properties

![[Pasted image 20220813140543.png]]

![[Pasted image 20220813140608.png]]

### Counting
Refer to [[Counting]]

### Probability Axioms
![[Pasted image 20220813164413.png]]

To prove A and B are mutually exclusive, prove $A \cap B = 0$

### Probability Proposition

1. P(empty set) = 0
2. If $A_1, A_2, ... A_n$ are *mutually exclusive event*, $$P(A_1\cup A_2\cup{} ... \cup A_n) = P(A_1) + P(A_2) +...P(A_n)$$ 
3. $P(A') = 1 - P(A)$
4. **Partition formula:** $$P(A) = P(A\cap B) + P(A\cap B')$$
5. $P(A \cup B) = P(A) + P(B) - P(A\cap B)$
6. $\text{If } A \subset B \text{ then } P(A) \leq P(B)$

### Finite Sample Space with Equally Likely Outcome

Consider sample space S = {$a_{1}, a_{2}, a_{3}...a_{k}$}

Assume all the outcomes in the sample space are *equaly likely* to occur:$$P(a_{1}) = P(a_{2}) = ... = P(a_{k})$$
Then for any event $A \subset S$,$$
P(A) = \frac{\text{No. sample points in A}} {\text{No. sample points in S}}$$
**Example:** If there are n people the room, what is the probability that there are **at least 2 people with the same birthday**?

sample space S = {all possible combinations of birthdays of n people} = S = 365 * 365 * ... = $365^{n}$
It is formed of equally likely sample points.

A = {at least 2 people share the same birthday} 
A' = {no one share the same birthday} = $365 * 364 * ... * (365 - (n - 1))$ 

**Since all the outcome is this sample space is equally likely to occur:**
P(A') = number of sample points in A / no. sample points in S 
= $\frac{365 * 364 * ... * (365 - (n - 1))}{365^{n}}$

P(A) = 1 - P(A') = 1 - (1 - $\frac{1}{365}$)(1- $\frac{2}{365}$)(...)(1 - $\frac{n - 1}{365}$)

![[Pasted image 20220816091433.png]]

### Conditional Probability
Refer to [[Conditional Probability]]

### Independence

Two events A and B are independent if and only if$$P(A\cap B) = P(A)P(B)$$Example: Flipping a coin and throwing a dice has no effect on each other.

Event A has no bearing on event B, hence $$A ⊥ B \iff P(A|B) = P(A)$$
Sometimes its **not obvious** that 2 events are independent! Must use formula to determine:

![[Pasted image 20220821184146.png]]
![[Pasted image 20220821184204.png]]

**Mutually exclusive** and **Independent** are 2 different concepts! 
- Mutual exclusiveness can be demonstrated on Venn diagram but Independence cannot.
- 2 events are both **mutually exclusive** and **independent** if at least one of them is an *empty set*. → Cannot occur at the same time otherwise.

![[Pasted image 20220821185209.png]]

### Partition

![[Pasted image 20220821185326.png]]

**Law of Total Probability:**$$P(B) = \sum_{i=1}^{n}P(B\cap A_{i}) = \sum_{i=1}^{n}P(A_{i})*P(B|A_{i})$$
Special Case:$$P(B) = P(B\cap A)+P(B\cap A') =P(A)P(B|A) + P(A')P(B|A')$$
Why does this work? Imagine all events in A are mutually exclusive to each others, and **they each overlaps with B at some regions** → The sum of all these regions is B.


Example: [[Monty-Hall Problem]]


### Bayes' Theorem

![[Pasted image 20220823120836.png]]

![[Pasted image 20220823120903.png]]

Remember that A and A' are partitions of S, meaning they are **mutually exclusive** events. 

## Slide
![[ST2334_Chapter_1_Slides.pdf]]

