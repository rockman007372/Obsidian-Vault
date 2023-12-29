---
tags: []
course: CS2109S
type: lecture
date: 2023-11-14 Tuesday
---
Given a dataset D and an error function, we can measure how well the model **h** performs through the **expected error** of the model:

![[Pasted image 20221117232317.png]]

The error function is called an evaluation metric. Some examples of evaluation metrics are:
- Accuracy
- Log Loss
- AUC-ROC

It is important to distinguish between **evaluation metrics** and **loss function**: 
- **Evaluation metrics** for a model explain the performance of a model
- **Loss functions** are used to optimize your model during training by minimizing the loss function via gradient descent.
- Some functions can be used for both purposes, but some are not.

![[Pasted image 20221117232807.png]]

We use the **training set** to train a series of models. We then use the **validation set** to choose the best-performing models. We then evaluate these models against the **test set** to see how well our models perform against external data.

To diagnose if our model is underfitting or overfitting:

![[Pasted image 20221117233605.png]]




---
Links:
