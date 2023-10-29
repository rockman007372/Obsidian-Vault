
A univariate linear function with input $x$ and output  $y$ has the form:
$$y = w_1x + w_0$$

Where `w0` and `w1` are real-valued coefficients to be learned. We can define **`w`** to be the vector `[w0, w1]` and define the hypothesis function:
$$h_w(x) = w_1x + w_0$$

The task of finding the $h_w$ that best fits the data is called **linear regression**. To fit a line to the data, all we have to do is find the values of the weights that **minimize the empirical loss**.

Since we can draw many best fit lines over the data, we follow **Occam's Razor Theorem** → prefer the **simplest** hypothesis that is consistent with the data.

One empirical cost function we can use is the **squared cost function**:
$$J(w_{0},w_{1})= \frac{1}{2m}\sum\limits^m_{i=1}(h_{w}(x^{(i)})-y^{(i)})^2$$
Where:
- m is the training set number $(x_1, y_2), (x_2, y_2), \text{...}$
- $x^{(i)}$ is the input i and $y^{(i)}$ is the corresponding output

Our goal is to pick $w_{0}, w_{1}$ such that $J(w_{0},w_{1})$ is minimised. Defining graph loss as a function of $w_0$ and $w_1$ in a three dimensional space, our goal is to find the coordinate of the **global minimum**.

![[Pasted image 20220919232206.png]]

Methods to find the weights that minimize loss:
- [[Gradient Descent]]
- [[Normalization]]