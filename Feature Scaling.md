
When features have significantly different scales, Gradient Descent does not work very well:
- Features with larger scales will affect the loss more significantly and influences the hypothesis curve more.
- Hence we scale the features so that they have roughly the same scale.

Some feature scaling techniques: 
- **Max-min scaling:** aim for $-1 \leq x_i \leq 1$
$$x_{i} = \frac{x_{i}-min(x_{i})}{max(x_{i}) - min(x_{i})}$$


- **Standard scaler:** 
$$x_i := \frac{x_{i}- \mu_{i}}{\sigma_{i}}$$
