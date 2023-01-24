---
tags: processed
course: CS2109S
type: lecture
date: 2022-10-19 Wednesday
---

Good [explanation](https://www.youtube.com/watch?v=ny1iZ5A8ilA)

## Notes

### Overfitting and Underfitting
[[Overfitting and Underfitting in ML]]

### Support Vector Machine

![[Pasted image 20221117225809.png]]

Big idea: SVM is also used for **classification** problem similar to [[Logistic Regression]]. However, while there many many distinct decision boundaries for Logistic Regression, SVM will give us the boundary that **maximise the margin** between the nearest data point from each class to the boundary.

![[Pasted image 20221117225843.png]]

Reason: Through some black math vector magic, by maximising the margin, we are minimizing the weights (regularization) at the same time. 

### Kernel Tricks

Big idea: Transform original data that is *linearly inseperable* to a higher plane so that there exists a boundary plane to separate the transformed data. 

![[Pasted image 20221117230825.png]]
![[Pasted image 20221117230855.png]]

### Hypothesis Evaluation

Given a dataset D and an error function, we can measure how well the model **h** performs through the **expected error** of the model:

![[Pasted image 20221117232317.png]]

The error function is called an evaluation metric. Some examples of evaluation metrics are:
- Accuracy
- Log Loss
- AUC-ROC

It is important to distinguish between evaluation metrics and **loss function**. **Evaluation metrics** for a model explain the performance of a model, but **loss functions** are used to optimize your model during training by minimizing the loss function using gradient-based training methods. Some functions can be used for both purposes, but some are not.

![[Pasted image 20221117232807.png]]

We use the **training set** to train a series of models. We then use the **validation set** to choose the best-performing models. We then evaluate these models against the **test set** to see how well our models perform against external data.

To diagnose if our model is underfitting or overfitting:

![[Pasted image 20221117233605.png]]


## Summary

## Questions/Cues

---
Links:
