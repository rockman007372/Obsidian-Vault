---
tags: processed
course: CS2109S
type: lecture
date: 2022-11-19 Saturday
---

## Notes

### 1-layer Perceptron

![[Pasted image 20221119222712.png]]

Examples of non-linear function g:
- Sigmoid: $$g(z) =\frac{1}{1 + e^{-z}}$$
- Step function: $$sgn(x)= 
\begin{cases}
    1& \text{if } x\geq 0\\
    -1 & \text{if } x < 0
\end{cases}
$$
- $tanh(x)$
- ReLU: $$max(0, x)$$
Comparison between Perceptron and Linear SVM in data classification:
![[Pasted image 20221119225254.png]]


| Single Perceptron                                             | Linear SVM                                              |
| ------------------------------------------------------------- | ------------------------------------------------------- |
| Not robust: Can select any model to linear, not deterministic | optimal stability by maximizing margin                  |
| Cannot converge on non-linearly seperable data                | Soft margin: Can learn from non-linearly separable data |

A single perceptron cannot classify non-linearly seperable data. However, we can use multi-layer neural network to do so.

![[Pasted image 20221120093916.png]]

Note that the activation functions should be non-linear to reap the benefits of multi-layer perceptrons. **Without non-linear activations, the entire network collapses to a simple linear model**. It’s as good as using a network with one layer; we can no longer capitalise on this "depth" of the original neural network, lowering the network's learning capacity.


### Gradient Descent for 1 perceptron with Sigmoid non-linear function

Perceptron function:$$\hat{y}=g(f(x))$$
Where g is the sigmoid function: $$g(z) =\frac{1}{1 + e^{-z}}$$
Loss function is MSE:$$J = \frac{1}{2}(\hat{y} -y)^{2}$$
Gradient descent:$$w_{i}= W_{i}- \alpha *\frac{dJ}{dw_{i}} = w_{i}- \alpha * (\hat{y} - y)*g'(f)*x_{i}$$
We can find derivative of sigmoid function g: $$g'(z) = \sigma'(z) = \sigma(z)(1 - \sigma(z))  $$
Hence, $$w_{i}= w_{i}- \alpha * (\hat{y} - y)*\hat{y}*(1-\hat{y})*x_{i}$$

### Neural Network (Multi-layer Perceptron)

![[Pasted image 20221120100037.png]]


Multi-layer perceptrons are sequences of matrix multiplication operations applied one after another. Hence the weight matrix dimensions flow into one another (commute well).

Given a 32 x 32 image, classify the image into 1 of the 4 classes:

![[Pasted image 20221120100801.png]]

### Forward propagation

![[Pasted image 20221120102102.png]]

Basically, passing the input through many layers of network to get  output $\hat{y}$

### Backward propagation

Big idea: Backpropation **efficiently** computes the gradient by
- Avoiding **duplicate** calculations - gradient descent on the network require a lot of duplicated intermediate derivatives.
- Compute the gradient of each layer from back to front (hence "backward"). 

We can just use automated differentiation in deep learning APIs (PyTorch) to do backward propagation.

### [[Deep Learning]]

## Summary

## Questions/Cues

---
Links:
