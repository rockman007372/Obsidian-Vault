---
tags: 
aliases: 
---
Date:: 2022-09-25 Sunday
Links: [[Basic Concept of Probability]]
- - -
# Conditional Probability

## Definition

$$P(B \text{ |} A) = \frac{ P(\text{B}\cap{A}) }{P(A)}$$

- P(B | A) is the probability of B given A has happened.
- Since we know A has occured, A is our new **reduced sampled space**

> Suppose two fair dice are rolled. Given that the first die is less than 3, what is the probability that the sum of the 2 dice is more than 7?

![[Pasted image 20220821182425.png]]

### Multiplication Rule

![[Pasted image 20220821182712.png]]

This is the fundamental principle of the **probability trees**. It allows us to calculate probability of consecutive actions:

![[Pasted image 20220821183228.png]]

### Connection between Independence and Conditional Probability

$$A ⊥ B \iff P(A|B) = P(A)$$
### Complement Rule 
$$P(A' |B) = 1 − P(A|B)$$ The prove proceeds as follow:

$$P(A'|B)=\frac{P(A'∩B)}{P(B)}=\frac{P(B)−P(A∩B)}{P(B)}=1−\frac{P(A∩B)}{P(B)}=1−P(A|B)$$

$P(A|B' )$ is *not the same* as $1 − P(A|B)$: The complement formula only holds with respect to the first argument. There is no corresponding formula for P(A|B'). However, you can **rely on the reliability of the test** to determine this information. 

## Sample questions

Sometimes to solve a conditional probability question, it is easier to look at the **reduced sample space** instead of blindly applying the formula!

Example:

> There are 18 first year, 15 second year, 10 third year and 5 fourth year students in the course TS4332. They are allocated randomly into 4 classes of 12 each. If there are a total of 6 first year and 8 second year students in classes A and B, what is the probability that class D has 4 first year and 4 second year students?

![[Conditional Probability 2022-09-25 22.54.15.excalidraw]]

 ---

When we talk about **reliability** of a test, we are talking about the P(Positive | Infect) and P(Positive | Uninfected) → Use reliability to get these information:

![[Pasted image 20220926012929.png]]

If no reliability is given, we follow the question: 

>An insurance company believes that people can be divided into two classes: accident prone and not accident prone. Historically, they observe that the probability that an accident prone person will have an accident within a fixed 1-year period is 0.04; **otherwise, the probability is 0.02**. Assume that 30% of the population is accident prone. 

In this question, P(A|P) = 0.04 and P(A|P') = 0.02.

---

Difficult question involving both independence and conditional probability:

![[Pasted image 20220926015534.png]]

Answer: 6/7
We use Bayes' Theorem and Independence.
P(win) = 1 / 2 = P(loss)
P(Arjun lies and Karan tells truth) = 1 / 3 x 1 / 4 = 1 / 12
P(Arjun tell truths and Karan lies) = 2 / 3 x 3 / 4 = 1 / 2
Applying Bayes Theorem: 
![[Conditional Probability 2022-11-17 15.54.36.excalidraw]]


