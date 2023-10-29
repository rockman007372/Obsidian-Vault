
Instead of modeling hypothesis as a univariate function, we can have hypothesis functions with multiple variables:

![[Pasted image 20220919235703.png]]

where:
- n is the number of feature
- $x^{(i)}$ is the input features (**a (n x 1) matrix**) of the $i^{th}$ training set
- $x_j^{(i)}$ is the value of feature j in the  $i^{th}$ training set

We can express hypothesis function as a **vector**:

![[Pasted image 20220920000358.png]]

We perform gradient descent in the generalised case similar to the univariate case:

![[Pasted image 20220920000502.png]]

### Feature Scaling 

When features have significantly different scales, Gradient Descent does not work very well:
- Features with larger scales will affect the loss more significantly and influences the hypothesis curve more.
- Hence we scale the features so that they have roughly the same scale.
- We try to aim for: $-1 \leq x_i \leq 1$

![[Pasted image 20220920001038.png]]

Another feature scaling tecnique is **mean normalizatiton**:

![[Pasted image 20220920001109.png]]