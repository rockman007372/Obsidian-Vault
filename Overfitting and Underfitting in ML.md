---
tags:
  - processed
course: CS2109S
type: lecture
date: 2022-11-17 Thursday
---

## Definition

![[Pasted image 20221117220220.png]]

![[Pasted image 20221117220237.png]]

- Underfitting = **high bias**: Model performs poorly on all data 
- Overfitting = **high variance**: Model performs well on training set but much worse on validation set and test set

![[Pasted image 20221117233158.png]]
![[Pasted image 20221117233803.png]]
## Address overfitting

1. Reduce the number of features: High degree polynomial → lower degree
2. Regularization: Penalise the weights to reduce their magnitude$$J(w ) = \frac{1}{2m}[\sum^{m}_{i=1}(h_{w}(x^{(i)}) - y^{(i)})^{2} + \lambda \sum^{n}_{i = 1}w_{i}^{2}]$$
Where $\lambda$ is some big value so that **gradient descent** will minimize weights. Notice that we do not penalise the bias term as $i\neq0$ .

#### Linear Regression with Regularization

![[Pasted image 20221117222933.png]]

#### Logistic Regression with Regularization

![[Pasted image 20221117223552.png]]

---
Links: [[CS2109S]], [[Support Vector Machine]]
