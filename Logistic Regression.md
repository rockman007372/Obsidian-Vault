---
tags: processed
course: CS2109S
type: lecture
date: 2022-10-19 Wednesday
---

A [[Supervised Learning]] model for classification problems.

The goal is to find the function of the **decision boundary** to separate datas.

![[Pasted image 20221117212725.png]]

After we transform the data based on the decision boundary function, we can use the function g to classify the data (binary outputs).

## Logistic Regression

### Hypothesis Function
$$h_{w}(x)=g(w^{T}x) = \frac{1}{1 + e^{-w^Tx}}$$
where $g(z)$ is the **sigmoid** function: 
$$ g(z) =\frac{1}{1 + e^{-z}}$$
and $h_{w}(x)$ represents the probability that y = 1 on input x.

![[Pasted image 20221117213432.png]]

### Cost Function

Cost of one sample:
$$Cost(h_{w}(x), y) = -y*log(h_{w}(x)) - (1 - y)*log(1 -h_{w}(x))$$

Average cost of m samples:
$$J(w) = -\frac{1}{m} \sum^{m}_{i=1} {y^{(i)}*log(h_{w}(x^{(i)})) + (1 - y^{(i)})*log(1 -h_{w}(x^{(i)})) }$$

Basically, when $y = 1$, we penalise $h_w(x)$ closer to 0 and vice versa.

### Gradient Descent
$$w_{n}:= w_{n}- \alpha*\frac{ 1}{m}\sum^{m}_{i=1}(h_{w}(x^{(i)})- y^{(i)})*x_{n}^{(i)}$$
Same as gradient descent in [[Linear Regression]]

## Multi-class Classification

![[Pasted image 20221117214425.png]]

1. Train a logistic classifier $h_{w}^{(i)}(x)$ for each class i to predict that y = i.
2. For each input x, pick the class i that maximise $h_w(x)$

## Summary

![[Pasted image 20221117213844.png]]


---
Links: [[CS2109S]]
