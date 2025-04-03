# Bessel's Correction

Bessel's Correction refers to when calculating [Standard Deviation](Standard%20Deviation.md), [Covariance](Covariance.md), and [Variance](Variance.md), a factor of $\frac{1}{n-1}$ is used instead of $\frac{1}{n}$.

## Intuitive explanation

When calculating the sample [Mean](Mean.md) from samples drawn from a population, the mean deviates from the population mean slightly, moving closer to the samples.

Therefore, spread from the sample mean is less than spread from the population mean. This causes the sample standard deviation, covariance, and variance to be _less_ than the population standard deviation, covariance, and variance. Hence, we use a factor of $\frac{1}{n-1}$ instead of $\frac{1}{n}$ to increase the sample standard deviation, covariance, and variance a bit so they are closer to the population standard deviation, covariance, and variance.

## Degree of freedom

In a data vector $\vec{x}$ of length $n$, we know that the total spread from the sample mean $x_i-\bar{x}$ sums to 0. Therefore, when we have $n-1$ spreads from the sample mean, the last one must add to the others to sum to 0. This means that one spread is dependent on the others. We say there is $n-1$ degrees of freedom.

