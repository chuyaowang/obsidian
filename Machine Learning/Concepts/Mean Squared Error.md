# Mean Squared Error

MSE measures the average of the squares of the residuals. It is essentially the [Residual Sum of Squares](Residual%20Sum%20of%20Squares.md) divided by the number of observations.

$$\text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$$

## Steps to Calculate RSS and MSE

1. **Compute the Residuals:**
   - For each observation, subtract the predicted value from the actual value to get the residual (error).

2. **Square the Residuals:**
   - Square each residual to ensure they are all positive values.

3. **Sum the Squared Residuals:**
   - Sum all the squared residuals to get the RSS.

4. **Calculate the Mean of the Squared Residuals:**
   - Divide the RSS by the number of observations to get the MSE.

### Example in Python

Here is a simple example using Python to calculate RSS and MSE:

```python
import numpy as np

# Example actual values and predicted values
y_actual = np.array([3, -0.5, 2, 7])
y_pred = np.array([2.5, 0.0, 2, 8])

# Calculate residuals
residuals = y_actual - y_pred

# Calculate RSS
rss = np.sum(np.square(residuals))
print(f"RSS: {rss}")

# Calculate MSE
mse = np.mean(np.square(residuals))
print(f"MSE: {mse}")
```

### Example in R

Here is a simple example using R to calculate RSS and MSE:

```r
# Example actual values and predicted values
y_actual <- c(3, -0.5, 2, 7)
y_pred <- c(2.5, 0.0, 2, 8)

# Calculate residuals
residuals <- y_actual - y_pred

# Calculate RSS
rss <- sum(residuals^2)
cat("RSS:", rss, "\n")

# Calculate MSE
mse <- mean(residuals^2)
cat("MSE:", mse, "\n")
```

## RSS vs. MSE
- **RSS (Residual Sum of Squares):** The sum of the squared differences between the actual and predicted values.
- **MSE (Mean Squared Error):** The average of the squared differences between the actual and predicted values.

Both metrics are useful for evaluating the accuracy of a regression model, with MSE providing a normalized measure that accounts for the number of observations.