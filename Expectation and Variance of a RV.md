---
tags: 
aliases: 
date: 2022-09-23 Friday
---

## Expectation of Discrete RV

Let X be a discrete RV with $R_{x}= \set{x_1, x_2, x_3,\cdot\cdot\cdot}$  and p.f. $f(x)$. The expectation or mean of X is defined as $$E(X) = \sum_{x_{i} \in R_{X}} x_i*f(x_{i})$$
## Expectation of Continuous RV

Let X be a continuous RV with p.f. f(x). The “expectation" or “mean " of X is defined by $$E(X) = \int_{-\infty}^{\infty} x*f(x) = \int_{x \in R_{X}} x*f(x)$$
## Properties of Expectation

Expectation expansion: $$E(aX + b) = aE(X) +b$$
Linearity of expectations: $$E(X + Y) = E(X) + E(Y)$$
Let g(X) be an arbitrary function:
$$E(g(X)) = \sum_{x_{i} \in R_{X}} g(x_i)*f(x_{i})$$
$$E(g(X)) = \int_{-\infty}^{\infty} g(x)*f(x) = \int_{x \in R_{X}} g(x)*f(x)$$

Note:
- Third rule is useful as we can manipulate $g(X)$ so that we can perform integration on the expectation expression eg. $$E(X) = E(X - 1 + 1) = E(X - 1) + 1$$
## Variance

Great revision [resource](https://www.ncl.ac.uk/webtemplate/ask-assets/external/maths-resources/statistics/descriptive-statistics/variance-and-standard-deviation.html#:~:text=The%20population%20variance%20is%20the,x1%2Cx2%2C%E2%80%A6)

Let $g(x) = (X - \mu_x)^2$. The variance of X is defined as $$\sigma^2= V(X) = E((X - \mu_x)^2)$$
![[Pasted image 20220923190459.png]]

### Properties of Variance

1. $V(X)$ is always non-negative:$$ V(X) \geq 0 , \forall X$$$$V(X) = 0 \iff P(X = E(X)) = 1\iff \text{X is a constant}$$
2. Expansion: $$V(aX + b) = a^{2}V(X)$$
3. Alternative formula: $$V(X) = E(X^{2})- (E(X))^{2}$$$$\sigma^{2}= V(X) = \frac{\sum_{i=1}^{n}(x_{i}-\mu)^{2}}{n}$$
- - -
Links: [[Random Variable]], [[Random Variables, Distributions, Expectations]]
