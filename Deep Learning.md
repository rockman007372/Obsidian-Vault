---
tags: processed
course: CS2109S
type: lecture
date: 2022-11-20 Sunday
---

## Notes

### Confusion Matrix

![[Pasted image 20221120105257.png]]


Precision measures type 1 errors:$$\text{Precision} = \frac{TP}{TP +FP}$$
Recall measures type 2 errors:$$\text{Recall} = \frac{TP}{TP + FN}$$
![[Pasted image 20221120105737.png]]

We cannot minimize both at the same time, hence we have to prioritize based on context.

However, we can use fair measurements to balance tradeoffs:$$\text{F1} = (\frac{P^{-1}+R^{-1}}{2} )^{-1}$$
### Receiver Operator Characteristic Curve (ROC)
![[Pasted image 20221120110645.png]]

Given the model output above, we can define a threshold $\pi = p$ and determine the True Positive Rate (TPR) and False Positive Rate (FPR). Repeat this for different thresholds to obtain the ROC curve.

![[Pasted image 20221120110856.png||500]]

The area under the curve (AUC) is a metric to evaluate how accurate the model is. $AUC > 0.5$
means the model is better than chance. $AUC = 1$ means the model is very accurate.


### Deep Learning

Deep learning is a neural network with many layers ($\geq 3$).

Data input has structures:
- Spatial structures: features within a vicinity have similar characteristics.
- Temporal Structures: features in adjacent time frames have similar characteristics.

To extract these features, we can use **CNN (Convolution Neural Network)** and **RNN (Recurrent Neural Network)**.

### Convolution NN

Key idea: Consider not only one pixel at a time, but a group of pixels.

![[Pasted image 20221120111731.png]]

![[Pasted image 20221120111804.png]]

A kernel is like a filter. Different kernel weights can extract different features. 

A convolution layer is used to extract the features into feature maps, which in turn are passed through linear layers in the neural network to produce predictions. 

![[Pasted image 20221120113212.png]]

##### Paddings and Stride

Padding is used to preserve the pixels at the edge of the image. We do this by adding 0 rows and columns surrounding the image pixels.

![[Pasted image 20221120112301.png]]

Stride is  used to speed up convolution, as computing adjacent filters might be too slow.  Instead of moving filter by 1 pixel, we can move the filter by a determined amount. This will reduce the size of the output feature map.

![[Pasted image 20221120112431.png]]


Formula to calculate kernel output dimensions:

Given padding P and stridding S, the width and height of the output, given kernel of dimension (K x K) and input of dimension (W x H) is: $$W_{1}= \lfloor{ \frac{W - K +2P}{S}}\rfloor + 1$$
$$H_{1}= \lfloor{ \frac{H - K +2P}{S}}\rfloor + 1$$
##### Pooling Layer

Given the feature maps produced by convolution layer, we can downsample it to help train kernels detect **higher-level** features. This also help reduces dimensionality (faster computation?).

![[Pasted image 20221120114407.png]]

Many pooling functions:
- Max-Pool
- Average-Pool
- Sum-Pool

### Recurrent Neural Network

Example: Predict tennis ball movement. We can learn about its path/trajectory from past predictions of its position.

![[Pasted image 20221120115208.png]]

Difference between Multi-Layer Perceptron vs RNN:

![[Pasted image 20221120115249.png]]


### Issues With Deep Learning

1. Overfitting 
2. Vanishing/Exploding Gradient


##### Overfitting
The neural network is too dense and complicated, learning the training set too well. Hence we can do **regularization** by randomly setting some activation to 0 to reduce the number of neurons.

![[Pasted image 20221121123152.png]]

##### Vanishing/Exploding Gradients
- Vanishing gradient: When we multiply many gradients between 0 and 1 during back propagation, the computed gradient is very small and hence the weights dont change.
- Exploding gradient: Gradients keep getting larger, causing gradient descent to diverge.

These can be solved by mitigation measures equivalent of feature scaling:
1. Proper Weight Initialization (random weights, not start with 0s)
2. Using Non-saturating functions (ReLU)
3. Batch Normalization
4. Gradient Clipping?

## Summary
![[Pasted image 20221120114601.png]]
## Questions/Cues

---
Links:
