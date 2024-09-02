# Bayesian Ridge Regression

Bayesian Ridge Regression is a probabilistic approach to linear regression. Unlike [standard ridge regression](L2%20Regularization.md), which penalizes large weights with a fixed regularization parameter, Bayesian Ridge Regression introduces a probabilistic framework that allows for uncertainty in the model parameters.

See also [The Bayesian View](MLE%20vs.%20Bayesian%20Parameter%20Estimation.md#The%20Bayesian%20View)
## Key Concepts:

1. **Probabilistic Model:**
   - Bayesian Ridge Regression models the weights as random variables with a prior distribution. Typically, a _Gaussian prior_ is used for the weights, which introduces regularization.
   - The model also includes a likelihood function that describes the probability of the observed data given the weights.

2. **Posterior Distribution:**
   - By combining the prior distribution and the likelihood function using Bayes' theorem, the posterior distribution of the weights is obtained. This posterior distribution captures the uncertainty about the weights given the observed data.

3. **Hyperparameters:**
   - Bayesian Ridge Regression includes hyperparameters for the precision (inverse of the variance) of the weights and the noise in the data. These hyperparameters can be estimated from the data using techniques such as empirical Bayes or Markov Chain Monte Carlo (MCMC).

4. **Regularization:**
   - The regularization effect in Bayesian Ridge Regression arises naturally from the prior distribution on the weights. This regularization helps prevent [Overfitting](Overfitting.md) and improves generalization.

## Prior, Likelihood function, posterior

In Bayesian Ridge Regression, using a Gaussian (normal) prior for the regression coefficients introduces regularization by incorporating _prior knowledge_ about the likely values of these coefficients. This approach effectively penalizes large coefficients, similar to how L2 regularization works in traditional ridge regression.

### Key Concepts

#### 1. **Gaussian Prior:**
   - The prior distribution for the regression coefficients $\mathbf{w}$ is assumed to be a Gaussian distribution centered at zero with a certain variance.
   - Mathematically, this can be expressed as:
     $p(\mathbf{w}) = \mathcal{N}(\mathbf{w} \mid \mathbf{0}, \tau^2 \mathbf{I})$
     where $\tau^2$ is the variance (precision $\lambda = \frac{1}{\tau^2}$) and $\mathbf{I}$ is the identity matrix.

#### 2. **Likelihood Function:**
   - The likelihood of the observed data given the coefficients is also modeled as a Gaussian distribution:
     $p(\mathbf{y} \mid \mathbf{X}, \mathbf{w}, \alpha) = \mathcal{N}(\mathbf{y} \mid \mathbf{X}\mathbf{w}, \alpha^{-1} \mathbf{I})$
     where $\alpha$ is the precision (inverse of the variance) of the **noise**.

#### 3. **Posterior Distribution:**
   - The posterior distribution of the coefficients $\mathbf{w}$ given the data is obtained using Bayes' theorem:
     $p(\mathbf{w} \mid \mathbf{X}, \mathbf{y}, \alpha, \tau) \propto p(\mathbf{y} \mid \mathbf{X}, \mathbf{w}, \alpha) \cdot p(\mathbf{w} \mid \tau)$
   - This posterior combines the likelihood of the data and the prior, balancing the fit to the data and the prior belief about the coefficients.

### Regularization Effect

The Gaussian prior acts as a form of regularization in the following ways:

1. **Penalizing Large Coefficients:**
   - The Gaussian prior $\mathcal{N}(\mathbf{w} \mid \mathbf{0}, \tau^2 \mathbf{I})$ has its peak at zero, meaning it assigns higher probabilities to smaller values of $\mathbf{w}$ and lower probabilities to larger values. This preference for smaller coefficients acts similarly to an L2 penalty in ridge regression.
   - In the Bayesian framework, this prior encourages the posterior distribution of the coefficients to be centered around zero unless the data strongly suggests otherwise.

2. **Regularization Term:**
   - When deriving the posterior, the negative log of the prior distribution $-\log p(\mathbf{w} \mid \tau)$introduces an additional term to the loss function, akin to the regularization term in ridge regression:
     $-\log p(\mathbf{w} \mid \tau) = \frac{1}{2\tau^2} \|\mathbf{w}\|^2 + \text{constant}$
   - This term directly penalizes the magnitude of the coefficients $\mathbf{w}$.

3. **Balancing Data and Prior:**
   - The posterior distribution represents a balance between the likelihood (fit to the data) and the prior (regularization). If the data strongly supports certain coefficient values, the posterior will reflect that. Otherwise, the prior will dominate, effectively shrinking the coefficients toward zero.

### Mathematical Derivation

To see this more formally, consider the Bayesian Ridge Regression loss function, which combines the likelihood of the data and the Gaussian prior:

$\mathcal{L}(\mathbf{w}) = \frac{\alpha}{2} \sum_{i=1}^n (y_i - \mathbf{w} \cdot \mathbf{x}_i)^2 + \frac{1}{2\tau^2} \sum_{j=1}^p w_j^2$

Here:
- The first term is the data fit term (scaled by precision of the noise $\alpha$).
- The second term is the regularization term (scaled by precision $1/\tau^2$).

Minimizing this loss function results in estimates of $\mathbf{w}$that balance fitting the data well while keeping the coefficients small, effectively achieving regularization.

## Relationship to L2 Regularization

Bayesian Ridge Regression is related to L2 regularization, but the terminology and conceptual framework are different. While L2 regularization explicitly uses the L2 norm in its penalty term, Bayesian Ridge Regression incorporates regularization through a probabilistic approach using Gaussian priors.
### Bayesian Ridge Regression

Bayesian Ridge Regression uses a Bayesian framework to introduce regularization. In this approach, the coefficients $\mathbf{w}$ are treated as random variables with a Gaussian prior:

$p(\mathbf{w}) = \mathcal{N}(\mathbf{w} \mid \mathbf{0}, \tau^2 \mathbf{I})$

This prior distribution assumes that the coefficients are normally distributed with mean zero and variance $\tau^2$, which introduces a preference for smaller coefficients. The regularization effect comes from the combination of the prior and the likelihood of the data.

### Relationship and Terminology

- **Implicit L2 Regularization:** Although Bayesian Ridge Regression does not explicitly add an L2 norm penalty term to the loss function, the Gaussian prior $\mathcal{N}(\mathbf{w} \mid \mathbf{0}, \tau^2 \mathbf{I})$ effectively imposes a similar constraint. The quadratic form of the Gaussian prior leads to a penalty on the sum of the squares of the coefficients, akin to the L2 norm.
- **Different Terminology:** In Bayesian Ridge Regression, the regularization is described in terms of prior distributions and posterior inference rather than as a direct penalty term. Thus, while it achieves similar regularization effects, it is not typically referred to as "L2 regularization." Instead, it is described in terms of Bayesian priors and posterior distributions.

## Implementation:

In Python's scikit-learn library, Bayesian Ridge Regression can be implemented as follows:

```python
from sklearn.linear_model import BayesianRidge

# Create a Bayesian Ridge regression model
model = BayesianRidge()
model.fit(X_train, y_train)

# Predict using the model
y_pred = model.predict(X_test)
```

## Non-informative Prior

In Bayesian Ridge Regression, a non-informative prior distribution refers to a prior distribution that exerts minimal influence on the posterior distribution, effectively allowing the data to dominate the inference process. This is particularly useful when there is little prior knowledge about the parameters. Here’s a detailed explanation:

### Non-Informative Priors

1. **Purpose**: 
   Non-informative priors are used when we want to avoid biasing the results with prior assumptions and instead rely primarily on the data to determine the posterior distribution.

2. **Forms of Non-Informative Priors**: 
   - **Uniform Prior**: One common type of non-informative prior is a uniform prior, which assigns equal probability to all values within a certain range. For instance, a uniform prior over the coefficients would imply that any value of the coefficient is equally likely before observing the data.
   - **Jeffreys Prior**: Another type of non-informative prior is the Jeffreys prior, which is invariant under reparameterization and often used for scale parameters. For a parameter $\theta$, the Jeffreys prior is proportional to the square root of the Fisher information.

### Bayesian Ridge Regression with Non-Informative Priors

In Bayesian Ridge Regression, we model the linear relationship between the predictors $X$ and the response $y$ with a Gaussian likelihood, and we place priors on the regression coefficients $\beta$ and the noise variance $\sigma^2$. 

1. **Model Specification**:
   $y \sim \mathcal{N}(X\beta, \sigma^2I)$
   $\beta \sim \mathcal{N}(0, \tau^2I)$
   $\sigma^2 \sim \text{Inverse-Gamma}(a, b)$

2. **Non-Informative Priors on $\beta$**:
   - A common choice for a non-informative prior on $\beta$ is a Gaussian prior with a very large variance, effectively making it close to a uniform distribution over a wide range.
   - $\beta \sim \mathcal{N}(0, \tau^2I)$
     Here, $\tau^2$ is set to a very large value, making the prior almost flat.

3. **Non-Informative Priors on $\sigma^2$**:
   - For the noise variance $\sigma^2$, a common non-informative prior is an Inverse-Gamma distribution with very small shape and scale parameters (close to zero), which spreads the probability over a wide range of values.
   - $\sigma^2 \sim \text{Inverse-Gamma}(\epsilon, \epsilon)$, with $\epsilon \rightarrow 0$.

### Implications of Non-Informative Priors

- **Data Dominance**: With non-informative priors, the posterior distribution is primarily influenced by the likelihood derived from the data, meaning that the resulting inference and parameter estimates are largely driven by the observed data rather than any strong prior beliefs.
- **Parameter Uncertainty**: Non-informative priors reflect high uncertainty about the parameter values before observing the data, making them a cautious choice when prior information is scarce or unreliable.

### Conclusion

Non-informative prior distributions in Bayesian Ridge Regression are designed to have minimal influence on the posterior, allowing the data to play the dominant role in determining the model parameters. This approach is particularly useful when there is little or no prior knowledge about the parameters, ensuring that the inference is primarily data-driven.