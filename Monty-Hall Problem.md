---
tags: probability
aliases: 
date: 2022-11-18 Friday
---

## Question
- Suppose you are on a game show, and you are given the choice of three doors: behind one door is a car; behind the others, goats. 
- You pick a door, say No. 1, and the host Monty, who knows what is behind the doors, opens another door, say No. 3, which has a goat. He then says to you, “Do you want to pick door No. 2?" 
- Is it to your advantage to switch your choice?

## Solution using Law of Total Probability

 Denote the events: 

 - W = {Win the car} 
 - A = {car is behind the door of the initial pick} 
 
 
 Then, our interest is P(W), i.e., the probability of wining the car. 
 
 Applying the law of total probability, we have $$P(W) = P(A)P(W|A) +P(A')P(W|A') = \frac{1}{3} P(W|A) + \frac{2}{3 }P(W|A')$$
If we stick with the same door, $P(W|A) = 1$, $P(W|A) = 0$.  Hence $P(W) = 1 /3$

Conversely, if we choose to switch door, $P(W) = 2/3$ → WE SHOULD SWITCH DOOR

---
Links: [[Basic Concept of Probability]]
