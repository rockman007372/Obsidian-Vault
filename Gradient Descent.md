
Gradient descent is a technique to find the global minimum in the **weight space** - the space defined by all possible settings of the weights. 

It is very similar to [[Hill Climbing]] from Local Search - We first start at some point $(w_0, w_1)$, pick a nearby point that reduces $J(w_0, w_1)$ and keep going until hopefully we arrive at global minimum.

![[Pasted image 20220919232629.png]]

Learning rule for the weights:

$$w_{j}← w_{j}- \alpha\frac{\partial{J(w_{0}, w_{1},...))}}{\partial{w_{j}}}$$
where:
- $\alpha$ is the learning rate, used to minimize the loss (determines how fast we descend down to the minimum) → Can be fixed or vary with gradient
- $\partial$ is the partial derivative - differentiation with respect to a **single variable**

Correct way to perform gradient descent:

![[Pasted image 20220919233315.png]]

In our univariate linear function $h(x) = w_0 + w_1x$:

![[Pasted image 20220919235121.png]]

##### Intuition of why this works

![[Pasted image 20220919233458.png]]

##### Choosing a good learning rate is important
If apha is too small, it will take a long time to reach minimum
![[Pasted image 20220919233912.png]]

If alpha is too large, values will fluctuate and overshoot.
![[Pasted image 20220919234002.png]]

![[Regression 2022-09-19 23.40.30.excalidraw||400x900]]

Ideally, alpha should **decrease** as gradient decreases:
- Initially, large alpha to speed up descent
- Nearing optimal value, slow down for more gradual convergence

##### Variants of Gradient Descent
- **Batch** Gradient Descent: Consider **all** training sets (ABOVE)
- **Stoichastic**: 
	- Only consider one data point at a time
	- Faster, but more random and can escape local minima