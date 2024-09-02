# Bagging Ridge Regression

Bagging Ridge Regression is an ensemble learning method that combines the predictions of multiple ridge regression models to improve the overall performance. "Bagging" stands for Bootstrap Aggregating, and it aims to reduce variance and prevent [Overfitting](Overfitting.md).

Bagging Ridge Regression Enhances the performance of [ridge regression](L2%20Regularization.md) by leveraging the power of ensemble methods, specifically by reducing variance and improving model stability.

## Key Concepts:

1. **Bootstrap Sampling:**
   - Multiple subsets of the training data are created by randomly sampling with replacement. Each subset is called a bootstrap sample.

2. **Ridge Regression Models:**
   - A separate ridge regression model is trained on each bootstrap sample. This results in multiple models that capture different aspects of the data.

3. **Aggregation:**
   - The predictions from all the ridge regression models are aggregated (usually by averaging) to produce the final prediction. This aggregation helps to reduce the variance of the predictions and improves robustness.

## Benefits:

- **Variance Reduction:** By averaging the predictions of multiple models, bagging reduces the variance and helps in creating a more stable and robust model.
- **Improved Performance:** Bagging often improves predictive performance, especially in cases where individual models have high variance.

#### Implementation:

In Python's scikit-learn library, Bagging Ridge Regression can be implemented using the `BaggingRegressor` with `Ridge` as the base estimator:

```python
from sklearn.ensemble import BaggingRegressor
from sklearn.linear_model import Ridge

# Create a Ridge regression model
ridge_model = Ridge(alpha=1.0)

# Create a Bagging regressor with Ridge as the base estimator
bagging_model = BaggingRegressor(base_estimator=ridge_model, n_estimators=10, random_state=0)
bagging_model.fit(X_train, y_train)

# Predict using the bagging model
y_pred = bagging_model.predict(X_test)
```
