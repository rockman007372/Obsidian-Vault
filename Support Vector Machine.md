---
tags: processed
course: CS2109S
type: lecture
date: 2022-10-19 Wednesday
---

Good [explanation](https://www.youtube.com/watch?v=ny1iZ5A8ilA)

![[Pasted image 20221117225809.png]]

- SVM is also used for **classification** problem similar to [[Logistic Regression]]. 
- While there many many distinct decision boundaries for Logistic Regression, SVM will give us the boundary that **maximise the margin** between the nearest data point from each class to the boundary.

![[Pasted image 20221117225843.png]]

Reason: Through some black math vector magic, by maximising the margin, we are minimizing the weights (regularization) at the same time. 

### Kernel Tricks

Big idea: Transform original data that is *linearly inseperable* to a higher plane so that there exists a boundary plane to separate the transformed data. 

![[Pasted image 20221117230825.png]]
![[Pasted image 20221117230855.png]]

