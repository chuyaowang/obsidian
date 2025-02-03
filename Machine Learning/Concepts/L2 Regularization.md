# L2 Regularization

[IBM post](https://www.ibm.com/topics/ridge-regression)

L2 regularization, or ridge regularization, Tikhonov regularization, or ridge regression, is a ML technique to prevent [Overfitting](Overfitting.md) by adding a penalty term to the loss function. The term is proportional to the sum of the squared values of the model's weights, thus penalizes **large weights**.

Ridge regression is also applied to multiple regression data that suffer from multicollinearity. When independent variables are highly correlated, the least squares estimates become _unbiased_, but their variances are _large_, which means that they may be far from the true value. Ridge regression addresses this issue by imposing a penalty on the size of the coefficients.

## General Form

The ridge regression estimate is defined as the minimization of the following objective function:

$\min_{\beta} \left( \| y - X\beta \|^2_2 + \lambda \| \beta \|^2_2 \right)$

Where:
- $y$ is the response variable.
- $X$ is the matrix of predictors.
- $\beta$ is the vector of coefficients.
- $\lambda$ is the regularization parameter.
- $\| y - X\beta \|^2_2$ is the residual sum of squares.
- $\| \beta \|^2_2$ is the sum of squares of the coefficients (also known as the L2 norm).

The key idea is to add a penalty term, $\lambda \| \beta \|^2_2$, to the ordinary least squares (OLS) objective. The parameter $\lambda$ controls the strength of the penalty. When $\lambda = 0$, ridge regression is equivalent to OLS. As $\lambda$ increases, the impact of the penalty term grows, leading to smaller coefficient estimates.

## Linear Model

In the context of a linear model, the regularized loss function with L2 regularization is defined as:

$$L(\mathbf{w}) = L_0(\mathbf{w}) + \lambda \sum_{j=1}^n w_j^2$$

where:

- $L(\mathbf{w})$ is the regularized loss function.
- $L_0(\mathbf{w})$ is the original loss function (e.g., mean squared error for regression).
- $\lambda$ is the regularization parameter that controls the strength of the penalty.
- $w_j$​ are the weights of the model.
- $n$ is the number of weights.

## Effects of L2 Regularization

### Advantages

1. **Shrinkage of Weights:** The penalty term $\lambda \sum_{j=1}^n w_j^2$​ forces the optimization process to keep the weights small, thus shrinking their values. This helps to prevent the model from fitting the noise in the training data.
2. **Smoothness:** By penalizing large weights, L2 regularization encourages smoother and more stable models, which are less sensitive to small changes in the input data.
3. **Bias-Variance Tradeoff:** L2 regularization introduces a tradeoff between bias and variance. While it may increase the bias slightly (leading to a simpler model), it significantly reduces the variance, thus improving the model's generalization performance.
	1. $\lambda$ controls the strength of regularization. The higher it is, the more bias introduced into the model, and the less variance there is.
	2. Mean square error (MSE) can help determine a suitable $\lambda$ value. MSE is closely related to residual sum of squares (RSS) and is a means of measuring the difference, on average, between predicted and true values. As $\lambda$ increases, MSE increases. Nevertheless, it is argued that there always exists a value of λ greater than zero such that MSE obtained through ridge regression is smaller than that obtained through OLS. One method for deducing a suitable λ value is to find the highest value for λ that does not increase MSE. Additional [cross-validation](https://www.ibm.com/docs/en/spss-modeler/18.0.0?topic=settings-cross-validation) techniques can help users select optimal λ values for tuning their model.
4. **Handles Multicollinearity**: Ridge regression can handle multicollinearity by imposing a penalty on the size of the coefficients, which helps to stabilize the estimation process.
5. **Informative Variable Selection**: Although L2 regularization does not perform variable selection in the strictest sense (like [L1 Regularization](L1%20Regularization.md), which can set some coefficients exactly to zero), it does help in highlighting informative variables. Variables that consistently have **non-zero**, **relatively large coefficients** after regularization are likely to be informative, as the regularization would have shrunk less important variables more significantly.

### Disadvantages

1. **Interpretability**: The coefficients are shrunk towards zero, making them harder to interpret.
2. **Choice of $\lambda$**: Selecting an appropriate value for $\lambda$ is crucial and can be done using techniques like cross-validation.

## Practical Implementation

In many machine learning libraries, L2 regularization can be easily applied by specifying the regularization parameter λ\lambdaλ. For example, in scikit-learn, L2 regularization is applied by default in models like `Ridge` regression and logistic regression.


``` python
from sklearn.linear_model import Ridge  

# Create a Ridge regression model with L2 regularization 
model = Ridge(alpha=1.0)  # alpha is the regularization parameter (lambda) 
model.fit(X_train, y_train)
```

In neural networks, L2 regularization can be applied to the weights during the optimization process. In Keras, for example:

``` python
from tensorflow.keras.models import Sequential 
from tensorflow.keras.layers import Dense 
from tensorflow.keras.regularizers import l2  

model = Sequential([     
	Dense(64, input_dim=input_dim, activation='relu', kernel_regularizer=l2(0.01)),     
	Dense(1, activation='linear', kernel_regularizer=l2(0.01)) 
	])  
model.compile(optimizer='adam', loss='mse') 
model.fit(X_train, y_train, epochs=100, batch_size=32)`
```

By adding L2 regularization, the model is less likely to overfit and should perform better on unseen data.

## Why avoid large weights?

Large weights in a machine learning model can be problematic for several reasons:

### 1. **Overfitting:**
   - **Sensitivity to Noise:** Large weights can make the model overly sensitive to the noise in the training data. This means that the model might fit the training data very well but perform poorly on new, unseen data because it has essentially memorized the training data rather than learning the underlying patterns.
   - **Complexity:** Large weights often correspond to complex decision boundaries. While this complexity might fit the training data closely, it can lead to poor generalization to new data.

### 2. **Stability:**
   - **Numerical Instability:** Models with large weights can become numerically unstable, especially in deep learning. This instability can lead to large changes in the output for small changes in the input, which is undesirable.
   - **Gradient Explosion:** In gradient-based optimization methods, large weights can cause gradients to explode, making the training process difficult and leading to convergence issues.

### 3. **Regularization and Generalization:**
   - **Bias-Variance Tradeoff:** Large weights typically reduce the bias but increase the variance of the model. High variance means the model is likely to change significantly with slight variations in the training data, indicating poor generalization.
   - **Regularization:** Techniques like L2 regularization penalize large weights, encouraging the model to learn simpler patterns that generalize better to new data. This regularization helps in achieving a balance between bias and variance.

### 4. **Interpretability:**
   - **Less Interpretability:** Models with large weights are often more complex and harder to interpret. This lack of interpretability can be a significant drawback, especially in applications where understanding the model's decisions is crucial (e.g., healthcare, finance).

### 5. **Physical Constraints:**
   - **Real-World Constraints:** In some applications, weights correspond to physical quantities. Large weights might imply unrealistic or impractical values that don't make sense in the real-world context.

### Example:

Consider a simple linear regression problem:

$y = w_1x_1 + w_2x_2 + \cdots + w_nx_n + b$

If the weights $w_1, w_2, \ldots, w_n$ are very large, a small change in any of the input features $x_i$ can lead to a large change in the output $y$. This makes the model highly sensitive to the input data, and such sensitivity is usually undesirable because it indicates that the model is not robust.

### Visualization:

Here's a visualization to illustrate the effect of large weights:

- **Without Regularization (Large Weights):**
  - The decision boundary is very complex.
  - The model fits the training data very closely, including the noise.
  - High variance and poor generalization to new data.

- **With Regularization (Smaller Weights):**
  - The decision boundary is smoother and simpler.
  - The model captures the underlying pattern in the data without fitting the noise.
  - Better generalization to new data.

In summary, large weights are often not desirable because they can lead to overfitting, instability, poor generalization, and less interpretable models. Regularization techniques like L2 regularization help mitigate these issues by penalizing large weights, encouraging the model to find simpler, more generalizable solutions.

## Why called ridge regression?

The term "ridge regression" originates from the way the solution to the regularized regression problem is visualized geometrically. 
### Geometric Interpretation

In standard linear regression, the solution corresponds to finding the point in the parameter space that minimizes the sum of squared residuals. When multicollinearity is present, this solution can be unstable and may lie in a "ridge" or elongated region of the parameter space where small changes in the data can lead to large changes in the estimated coefficients.

### Regularization and the Ridge

Ridge regression adds a penalty term to the sum of squared residuals, which effectively shrinks the coefficients towards zero. This penalty term is based on the L2 norm of the coefficients, $\| \beta \|^2_2$. The constraint imposed by the regularization term can be visualized as adding an ellipsoidal contour (or ridge) to the error surface. The ellipsoid is centered at the origin, and its shape is determined by the regularization parameter $\lambda$.

### Visual Analogy

- **Ordinary Least Squares (OLS)**: The solution lies at the point where the residual sum of squares is minimized. This can be visualized as finding the point at the bottom of a bowl-shaped error surface.
- **Ridge Regression**: The solution lies at the point where the residual sum of squares plus the penalty term is minimized. This can be visualized as finding the point on the ridge of the ellipsoidal contour that intersects the bowl-shaped error surface.

The term "ridge" reflects the added stability and control over the solution provided by the regularization term, which helps prevent the solution from lying on an unstable, elongated region of the parameter space.
## L2 regularization for other models

### Non-Linear Models

#### 1. Polynomial Regression

Polynomial regression is a type of non-linear regression where the relationship between the independent variable $x$ and the dependent variable $y$ is modeled as an $n$-degree polynomial.

$y = w_0 + w_1 x + w_2 x^2 + \cdots + w_n x^n$

L2 regularization can be added to the polynomial regression model by including the penalty term:

$\text{Loss}_{\text{regularized}} = \frac{1}{2m} \sum_{i=1}^m (y_i - \hat{y}_i)^2 + \lambda \sum_{j=1}^n w_j^2$

#### 2. Support Vector Regression (SVR)

Support Vector Regression (SVR) is a type of regression model that uses support vector machines (SVMs) for regression tasks. SVR can be kernelized to handle non-linear relationships. L2 regularization is commonly used in SVR to penalize the magnitude of the coefficients:

$\text{Loss}_{\text{regularized}} = \frac{1}{2} \sum_{i=1}^m \max(0, |y_i - \hat{y}_i| - \epsilon) + \frac{1}{2} \sum_{j=1}^n w_j^2$

#### 3. Neural Networks

Neural networks are highly flexible non-linear models that can learn complex relationships between inputs and outputs. L2 regularization, also known as weight decay in the context of neural networks, can be applied to the weights of the network:

$\text{Loss}_{\text{regularized}} = \text{Loss}_{\text{original}} + \lambda \sum_{j=1}^n w_j^2$

In this case, the regularization term is added to the original loss function (e.g., cross-entropy loss or mean squared error).

### Implementation in Python

L2 regularization can be implemented using various machine learning libraries in Python. Here are examples for polynomial regression, SVR, and neural networks:

#### Polynomial Regression with L2 Regularization

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.linear_model import Ridge
from sklearn.pipeline import make_pipeline

# Example data
X = [[1], [2], [3], [4], [5]]
y = [1, 4, 9, 16, 25]

# Create a polynomial regression model with L2 regularization
degree = 3
model = make_pipeline(PolynomialFeatures(degree), Ridge(alpha=1.0))
model.fit(X, y)
y_pred = model.predict(X)
```

#### Support Vector Regression with L2 Regularization

```python
from sklearn.svm import SVR

# Example data
X = [[1], [2], [3], [4], [5]]
y = [1, 4, 9, 16, 25]

# Create a support vector regression model with L2 regularization
model = SVR(kernel='poly', degree=3, C=1.0)
model.fit(X, y)
y_pred = model.predict(X)
```

#### Neural Networks with L2 Regularization

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
from tensorflow.keras.regularizers import l2

# Example data
import numpy as np
X = np.array([[1], [2], [3], [4], [5]])
y = np.array([1, 4, 9, 16, 25])

# Create a neural network model with L2 regularization
model = Sequential([
    Dense(10, activation='relu', kernel_regularizer=l2(0.01), input_shape=(1,)),
    Dense(1, kernel_regularizer=l2(0.01))
])

model.compile(optimizer='adam', loss='mse')
model.fit(X, y, epochs=100, verbose=0)
y_pred = model.predict(X)
```

## L2 norm

L2 regularization gets its name from the L2 norm, which is also known as the [Euclidean norm](Euclidean%20Norm.md). The L2 norm of a vector is defined as the square root of the sum of the squares of its components (like how the Euclidean distance is calculated). 

### L2 Norm

For a vector $\mathbf{w} = [w_1, w_2, \ldots, w_n]$, the L2 norm is defined as:

$\| \mathbf{w} \|_2 = \sqrt{w_1^2 + w_2^2 + \cdots + w_n^2}$

### L2 Regularization in the Context of Machine Learning

In the context of regularizing a regression model, L2 regularization involves adding a penalty term to the loss function that is proportional to the L2 norm of the coefficients (without the square root for simplicity). This penalty term is the sum of the squares of the coefficients:

$\lambda \sum_{j=1}^n w_j^2$

Here, $\lambda$ is the regularization parameter that controls the strength of the penalty.

### Mathematical Formulation

For a linear regression model, the standard loss function (mean squared error) without regularization is:

$L_0(\mathbf{w}) = \frac{1}{2m} \sum_{i=1}^m (y_i - \mathbf{w} \cdot \mathbf{x}_i - b)^2$

When we add L2 regularization, the loss function becomes:

$L(\mathbf{w}) = \frac{1}{2m} \sum_{i=1}^m (y_i - \mathbf{w} \cdot \mathbf{x}_i - b)^2 + \lambda \sum_{j=1}^n w_j^2$

In this regularized loss function, the term $\lambda \sum_{j=1}^n w_j^2$ is the L2 regularization term. It penalizes large values of the weights $w_j$, encouraging them to be small.

