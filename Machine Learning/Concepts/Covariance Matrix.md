# Covariance Matrix

Given a $n\times p$ matrix $X$, its covariance matrix defines the [Covariance](Covariance.md) between each column of $X$ and the [Variance](Variance.md) of each column of $X$.

The covariance matrix is calculated as $$\operatorname{Cov}(X)=\frac{1}{n-1}X^TX$$, where $n$ is the number of samples, and $X$ is the mean centered matrix $X$.

## Characteristics

- Symmetric: the covariance matrix is always symmetric.