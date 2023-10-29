
Besides linear regression, hypothesis can also be modelled as a polynomial regression:

![[Pasted image 20220920001607.png]]

In real-world data, a straight line might not fit the data perfectly. Consider the relation between **number of schools nearby** and **asking price of a house**.

Houses with 0 schools nearby tend to be cheaper than houses with 1 school nearby. However, **as the number of schools increases, the increase in prices decrease**. A polynomial function can better capture this relationship. A polynomial function is written as follows:
$$ y = w_0 + w_1 x + w_2 x^2 + ... + w_n x^n $$

where $y$ is the target value, $x$ is a (*single*) feature value, and $n$ is the degree of the polynomial. $w_0$ and $w_1, \dots, w_n$ are as before.

- We can find the weights using either gradient descent or normalization.
- The polynomial does not have to be discrete → Instead of $x^3$, we can perhaps have $\sqrt{x}$
- As we create a higher degree polynomial matrix, each column will have a larger scale than the previous one. This can lead to poor performance for gradient descent → solved using **feature scaling** 