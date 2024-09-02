# Multicollinearity

Multicollinearity refers to a situation in which two or more predictor variables in a multiple regression model are highly correlated, meaning that one predictor variable can be linearly predicted from the others with a substantial degree of accuracy. This situation can lead to several issues in the estimation of regression coefficients using ordinary least squares (OLS). Here’s why multicollinearity causes the effects mentioned:

## Unbiased Estimates with High Variance

1. **Unbiased Estimates**:
   - OLS estimates are unbiased, meaning that the expected value of the estimated _coefficients_ is equal to the true value of the _coefficients_. This property holds regardless of multicollinearity.
   - Mathematically, if $\beta$ is the true coefficient vector, then $\mathbb{E}[\hat{\beta}] = \beta$.

2. **High Variance**:
   - When predictor variables are highly correlated, the matrix $X^TX$ (where $X$ is the matrix of predictor variables) becomes close to singular, meaning it is nearly non-invertible.
   - The variance of the OLS estimator $\hat{\beta}$ is given by:
     $\text{Var}(\hat{\beta}) = \sigma^2 (X^TX)^{-1}$
     where $\sigma^2$ is the variance of the error term.
   - If $X^TX$ is close to singular, the entries of $(X^TX)^{-1}$ can become very large. This results in large variances for the coefficient estimates $\hat{\beta}$.
   - High variance implies that the coefficient estimates $\hat{\beta}$ can **vary widely with different samples**, even if the true underlying relationship is stable.

## Effects of Multicollinearity

1. **Instability of Coefficient Estimates**:
   - High variance in the coefficient estimates leads to instability. Small changes in the data can cause large changes in the estimates of the coefficients. This makes the model _sensitive to the particular sample used_.
   
2. **Interpretation Difficulties**:
   - When predictors are highly correlated, it becomes difficult to assess the individual effect of each predictor on the response variable. The estimated coefficients may not accurately reflect the true relationship between each predictor and the response.
   
3. **Increased Standard Errors**:
   - The standard errors of the coefficients increase due to multicollinearity. Larger standard errors mean wider confidence intervals for the coefficients, making it harder to determine if a predictor is statistically significant.

### Why Multicollinearity Causes These Effects

1. **Redundancy in Information**:
   - When predictors are highly correlated, they provide redundant information about the response variable. The model cannot distinguish the unique contribution of each predictor to the response.
   
2. **Numerical Instability**:
   - The near-singularity of $X^TX$ leads to numerical instability in computing the inverse of this matrix, which is required for estimating the coefficients. This instability manifests as large variances in the estimates.

### Ridge Regression as a Solution

[Ridge regression](L2%20Regularization.md) addresses the problem of multicollinearity by adding a penalty term to the loss function, which shrinks the coefficient estimates. This penalty term is controlled by the regularization parameter $\lambda$:

$\hat{\beta}_{\text{ridge}} = \arg \min_{\beta} \left( \| y - X\beta \|^2_2 + \lambda \| \beta \|^2_2 \right)$

- The ridge penalty $\lambda \| \beta \|^2_2$ stabilizes the inversion of $X^TX$ by making the problem better conditioned.
- It reduces the variance of the coefficient estimates at the cost of introducing some bias (biased but with lower variance), leading to more reliable and interpretable models.

In summary, multicollinearity causes high variance in OLS estimates because it makes the predictor matrix $X$nearly singular, leading to instability in the coefficient estimates. Ridge regression mitigates this issue by adding a penalty term, which regularizes the estimates and reduces their variance.

## Coefficient Variance

Reducing coefficients does not necessarily reduce variance. The relationship between the size of the coefficients and their variance depends on several factors, including the presence of multicollinearity, the amount of regularization applied, and the structure of the data. 

### Factors Affecting Coefficient Variance

1. **Multicollinearity**:
   - When predictors are highly correlated, even small changes in the data can lead to large changes in the estimated coefficients. This results in high variance, regardless of whether the coefficients themselves are small or large.
   - For example, in a situation of perfect multicollinearity, the coefficients can be arbitrarily large or small with very high variance.

2. **Regularization**:
   - Techniques like ridge regression (L2 regularization) shrink the coefficients by adding a penalty proportional to the sum of the squares of the coefficients. This reduces the variance of the coefficients.
   - However, regularization introduces bias. While regularized coefficients are generally smaller and have reduced variance compared to their unregularized counterparts, this does not imply that all small coefficients have small variance.

3. **Sample Size and Data Structure**:
   - The variance of the coefficient estimates also depends on the sample size and the variability in the data. Larger sample sizes tend to _reduce_ the variance of the estimates.
   - The design matrix $X$ (the matrix of predictors) influences the variance. If the columns of $X$ are nearly linearly dependent (indicating multicollinearity), the variance of the coefficients increases.

### Mathematical Perspective

The variance of the OLS estimator $\hat{\beta}$ is given by:
$\text{Var}(\hat{\beta}) = \sigma^2 (X^TX)^{-1}$
where $\sigma^2$ is the variance of the error term, and $X^TX$ is the matrix of predictors. The elements of $(X^TX)^{-1}$ can be large if $X$ is close to being singular, leading to high variance in $\hat{\beta}$.

In ridge regression, the estimator is:
$\hat{\beta}_{\text{ridge}} = (X^TX + \lambda I)^{-1}X^Ty$
Here, the addition of $\lambda I$ to $X^TX$ stabilizes the inversion, reducing the variance of $\hat{\beta}_{\text{ridge}}$. This often results in smaller coefficients, but it is the regularization that reduces variance, not the size of the coefficients themselves.

### Intuitive Example

Consider two different scenarios with a simple linear model:

1. **Scenario with Multicollinearity**:
   - Predictors $X_1$ and $X_2$ are highly correlated. Even if the true coefficients are small (say $\beta_1 = 0.1$ and $\beta_2 = 0.2$), the high correlation means the estimates of $\hat{\beta}_1$ and $\hat{\beta}_2$ will have high variance. Small coefficients in this case do not imply small variance.

2. **Scenario with Regularization**:
   - Applying ridge regression with a suitable $\lambda$ reduces the magnitude of the coefficients and stabilizes their estimates. Here, the small coefficients result from the regularization process, which also reduces variance. But this is a controlled scenario where small coefficients are associated with reduced variance due to regularization.

### Conclusion

While regularization techniques like ridge regression can produce smaller coefficients with reduced variance, small coefficients in general do not imply small variance. The relationship between coefficient size and variance is influenced by multicollinearity, regularization, sample size, and the structure of the data. Understanding these factors is crucial in interpreting the estimates and their variances in regression models.

## Stability of Inversion

Stabilizing an inversion refers to improving the numerical stability and conditioning of the matrix inversion process, especially in the context of solving systems of linear equations or estimating parameters in regression models. This is particularly important when dealing with nearly singular or ill-conditioned matrices, where direct inversion can lead to large numerical errors and unstable solutions.

### Context in Regression

In the context of ridge regression, stabilizing the inversion relates to making the matrix $X^TX$ (the Gram matrix of the predictor variables) better conditioned, so that the inversion required to solve for the regression coefficients is more stable and reliable.

### Ordinary Least Squares (OLS) Regression

In OLS regression, the coefficients $\hat{\beta}$ are estimated using the formula:
$\hat{\beta} = (X^TX)^{-1}X^Ty$

If $X^TX$ is nearly singular or ill-conditioned, the inversion $(X^TX)^{-1}$ can be numerically unstable. **Small changes in the data can cause large changes in the coefficients**, leading to **high variance in the estimates**.

### Ridge Regression

Ridge regression addresses this problem by adding a regularization term to the diagonal of $X^TX$:
$\hat{\beta}_{\text{ridge}} = (X^TX + \lambda I)^{-1}X^Ty$

Here, $\lambda$ is the regularization parameter, and $I$ is the identity matrix. This addition has several effects:

1. **Improved Conditioning**: The matrix $X^TX + \lambda I$ is better conditioned than $X^TX$. Conditioning refers to the _sensitivity of the solution to changes in the input data_. A well-conditioned matrix has a smaller condition number, meaning it is less sensitive to small changes or errors in the data.

2. **Numerical Stability**: The inversion $(X^TX + \lambda I)^{-1}$ is more stable because the _added term_ $\lambda I$ ensures that the matrix is not close to singular. This reduces the risk of _large numerical errors_ during the inversion process.

3. **Shrinkage**: The regularization term $\lambda I$ shrinks the coefficients towards zero, which helps to reduce their variance. This shrinkage is controlled by the regularization parameter $\lambda$. As $\lambda$ increases, the coefficients are shrunk more, and the inversion becomes more stable.

### Why Stabilizing the Inversion Matters

- **Numerical Precision**: Computers have finite precision, and operations like matrix inversion can introduce numerical errors. Stabilizing the inversion helps to minimize these errors.
- **Model Reliability**: Stable inversion leads to more reliable coefficient estimates. In the presence of multicollinearity, ridge regression provides more consistent and interpretable results.
- **Reduced Variance**: By stabilizing the inversion, ridge regression reduces the variance of the coefficient estimates, making the model less sensitive to small changes in the data.

### Example

Consider a simple example with two highly correlated predictors $X_1$ and $X_2$:

1. **OLS Regression**:
   $\hat{\beta} = (X^TX)^{-1}X^Ty$
   If $X_1$ and $X_2$ are highly correlated, $X^TX$ is nearly singular, and the inversion is unstable, leading to high variance in $\hat{\beta}$.

2. **Ridge Regression**:
   $hat{\beta}_{\text{ridge}} = (X^TX + \lambda I)^{-1}X^Ty$
   The term $\lambda I$ makes $X^TX + \lambda I$ well-conditioned, ensuring that the inversion is stable and the estimates $\hat{\beta}_{\text{ridge}}$ have lower variance.

In summary, stabilizing an inversion involves improving the numerical stability and conditioning of the matrix inversion process, making it more reliable and reducing the variance of the estimates. Ridge regression achieves this by adding a regularization term, which ensures the matrix to be inverted is better conditioned.