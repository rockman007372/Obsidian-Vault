---
tags: processed
course: CS2109S
type: lecture
date: 2022-09-07 Wednesday
---
Link: [[CS2109S]]
Crazy detailed [article](https://www.xoriant.com/blog/decision-trees-for-classification-a-machine-learning-algorithm)
- - - 
Decision Trees are a type of **Supervised** Machine Learning (that is you explain what the input is and what the corresponding output is in the training data) where the **data is continuously split according to a certain parameter**. 

The tree can be explained by two entities, namely decision nodes and leaves. The leaves are the decisions or the final outcomes. And the decision nodes are where the data is split.

![[Pasted image 20220913001220.png]]

There are 2 main types of Decision Trees:
1. **Classification Trees** (Yes/No) → The decision variable is Categorical
2. **Regression Trees** (Continuous Data)

To construct a good decision tree, we need to choose the parameter (attribute) widely!
- We want more compact tree, where a predicate can lead to all positive or negative outcomes
- To do this, we need the concept of Information Gain and Entropy.

## Information Value

The standard unit of information is the **bit**: $$I = -log_2(p)$$
where p is the probability of getting positive results out of all possible results.

Intuitively, $I$ measures the number of time we have **cut down our information in half**:
- If we cut the search space in half ($1 / 2$ of the original search space), $I = 1$ bit.
- If we cut the search space further in half ($1 / 4$ of the orginal search space),  $I = 2$ bits...

Why do we use the bit $I$:
1. $I$ is much greater than the probability of something very unlikely to happen → Easier to handle
2. We can do addition on bits just like how we do multiplication on probability
	- If the first guess cuts down space to $\frac{1}{4}$ of the original and the next guess cuts down space to $\frac{1}{2}$ of the first guess space:$\text{the total of information gain}= 2 \text{ bits} + 1 \text{ bits} = 3\text{ bits}$
	- In other word, we have reduced our search space to ${(\frac{1}{ 2}})^3=\frac{1}{ 8}$ of the original search space.

## Entropy

Entropy, also called as Shannon Entropy is denoted by H(S) for a finite set S, is the measure of the amount of **uncertainty** or randomness in data.$$H(S) = - \sum_{x \in X} \ p(x) \ *\log_2\ p(x) $$
Intuitively, it tells us about the **predictability of a certain event**. Example, consider a coin toss whose probability of heads is 0.5 and probability of tails is 0.5. Here the entropy is the highest possible, since there’s no way of determining what the outcome might be. 

Alternatively, consider a coin which has heads on both the sides, the entropy of such an event can be predicted perfectly since we know beforehand that it’ll always be heads. In other words, this event has **no randomness** hence it’s entropy is zero. In particular, **lower values imply less uncertainty while higher values imply high uncertainty.**

![[Pasted image 20220918194208.png]]

See [[Wordle Solver Heuristic]] to see an example of how entropy is used in determining the best guess word that gives the most information.

### Information Gain
Information gain is also called as Kullback-Leibler divergence denoted by $IG(S,A)$ for a set S is the **effective change in entropy** after deciding on a particular attribute A. It measures the relative change in entropy with respect to the independent variables
$$IG(S, A) = H(S) - \sum\limits_{i = 0}^{n}P(x)*H(x) = H(S) - Remainder(A)$$
where:
- $IG(S, A)$ is the information gained by applying feature A (Choosing A as predicate).  
- H(S) is the entropy of the current set (node)
- Second term is the entropy after applying feature A (the child node due to A) = the remainder of A

### ID3 DTL Algorithm

Recursive algorithm to create the most ideal decision tree:
1.  Create root node for the tree
2.  If all examples are positive, return leaf node ‘positive’
3.  Else if all examples are negative, return leaf node ‘negative’
4.  Calculate the entropy of current state H(S)
5.  For each attribute, calculate the entropy with respect to the attribute ‘x’ denoted by H(S, x)
6.  Select the attribute which has **maximum value of IG(S, x)**
7.  Remove the attribute that **offers highest IG** from the set of attributes
8.  Repeat until we run out of all attributes, or the decision tree has all leaf nodes.

Example:

![[Pasted image 20220913005312.png]]

![[Pasted image 20220913005321.png]]

![[Intro to Machine Learning 2022-09-13 00.57.13.excalidraw]]

Intuition: We want to **maximise information gain** by **minimizing the entropy of the next move** → Lower entropy means less randomness, hence more likely to determine the outcome!

## Summary
1.  Entropy to measure discriminatory power of an attribute for classification task. It defines the amount of randomness in attribute for classification task. **Entropy is minimal** means the attribute appears close to one class and has a **good discriminatory power** for classification
2.  Information Gain to **rank attribute** for filtering at given node in the tree. The ranking is based on high information gain entropy in decreasing order.
3.  The recursive ID3 algorithm that creates a decision tree.