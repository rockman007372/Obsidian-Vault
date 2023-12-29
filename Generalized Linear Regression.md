
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

