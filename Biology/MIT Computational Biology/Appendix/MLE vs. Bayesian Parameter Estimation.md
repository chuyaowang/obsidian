# MLE vs. Bayesian Views on Probability

> [TDS blog: overview of frequentist and Bayesian view](https://medium.com/trusted-data-science-haleon/priors-to-p-values-bayesian-vs-frequentist-perspectives-on-probability-300857a2ea62)
> [TDS blog: MLE and Bayesian parameter estimation](https://medium.com/towards-data-science/maximum-likelihood-vs-bayesian-estimation-dd2eb4dfda8a)

## Two world views

The frequentist and Bayesian views are two fundamentally different interpretations of *the kind of uncertainty* that probability is used to describe.

The frequentist view on probability believes there is true randomness. Probability describes the uncertainty due to randomness. In a coin flip example, the frequentist view regards P(head) as the number of times the coin lands on head if it is flipped for many times. Probability in the frequentist view is called **objective probability**.

The Bayesian view on probability does not believe in true randomness. Probability describes the uncertainty due to not having enough information. If I could factor in the coin's material, the wind speed, the tosser's hand movement, etc., I might estimate P(head) to be 80%. Probability in the frequentist view is called **subjective probability**.

## The Frequentist View

Probability in the frequentist view describes random events. However, parameters and hypotheses are not random. How can we estimate parameters and make inferences on hypotheses?
### Maximum Likelihood Estimation of Parameters

> [!summary] Likelihood Function
> $$
> L(\theta) = p(D|\theta)
> $$
> The likelihood function $L(\theta)$ is defined to be the probability of observing the data $D$ given the parameters $\theta$.

A likelihood curve can be calculated by plugging in the parameter $\theta$ into the probability distribution. The x axis is the range of parameters. The y axis is the likelihood. The parameter that **maximizes** the likelihood makes the observed data most probable under the assumed statistical model.

To get the parameters, take the derivative of $p(D|\theta)$ and find the $\theta$ that maximizes the likelihood.

> [!note] What MLE does not tell
> It is important to note that MLE does not tell us about the probability of the parameters being **true** given the data, i.e. $p(\theta|D)$, only an estimate of the parameters that maximizes the likelihood of observing the data.

Confidence intervals can be constructed for the estimated parameters. A 95% confidence interval has a 95% chance of containing the true parameters.

> [!note] Confidence Interval
> Note that the x% confidence of a confidence interval is the chance that your interval captures the true mean, and not that the true value falls in the interval. This is because the true parameter is fixed. It either falls in the interval or it does not.

### Null Hypothesis Significance Testing

Similarly, we cannot talk about the probability of a hypothesis being true because a hypothesis is not random. Instead, we talk about the probability of observing the data given the null hypothesis

$$
L(Null) = p(D|Null)
$$

For statistical inference, like the t-test, we calculate the probability of observing the data if the null hypothesis is true. If this probability is very small (<0.05), we reject the null hypothesis.

## The Bayesian View

The Bayesian approach calculates the probability distribution of the parameters being the one that generates the data. It is also a way to update beliefs or probabilities based on new evidence.

> [!summary] The Bayes Theorem
> The Bayes Theorem:
> $$
> p(\theta|D) = \frac{p(D|\theta)p(\theta)}{p(D)}
> $$
> $p(\theta|D)$: posterior
> $p(D|\theta)$: likelihood
> $p(\theta)$: prior
> $p(D)$: evidence, constant of integration

^e7c1f2

- The **posterior** is the probability distribution about the parameters of a statistical model after observing the data.
- The **likelihood** is the probability of observing the data given the parameters $\theta$. It represents the consistency between the evidence (data) and parameter values.
- The **prior** is the probability distribution that represents the initial belief or uncertainty about the parameters of a statistical model before observing any data. It comes from existing knowledge.
	- The prior is usually the same type of distribution as the posterior. This is known as *conjugate prior*. This assumption simplifies computation.
- The **constant of integration** is the marginal probability of observing the data across all possible parameter values. It serves to scale the likelihood\*prior to between 0 and 1.
- The posterior is the likelihood influenced by the prior belief and scaled by the constant of integration.

### Bayesian Estimation

$$
p(\theta|D) = \frac{p(D|\theta)p(\theta)}{\int p(D|\theta)p(\theta)d\theta}
$$

> [!info] Why P(D) is Replaced
> 1.  _P(D)_ is extremely difficult to actually calculate
> 2.  _P(D)_ doesn’t rely on θ, which is what we really care about
> 3.  Its usability as a normalizing factor can be substituted for the integral value, which ensures that the integral of the posterior distribution is 1.

For parameter estimation: use distributions and probability density functions in place of numerical probabilities.
- $p(\theta|D)$: posterior distribution
- $p(D|\theta)$: likelihood function
- $p(\theta)$: prior distribution 

### The prior

The prior can be hard to define as a probability distribution. It is also argued that since different prior beliefs will lead to different posteriors, the Bayesian approach is not scientific enough. The counter argument says that many subjective choices are already made in conducting an experiment.

### The constant of integration

It is sometimes hard to calculate or even intractable. When it cannot be calculated the Bayesian approach cannot be used.

An alternative way is to use Markov Chain Monte Carlo (MCMC) sampling, a method that provided a way to estimate the posterior distribution without having to calculate the constant of integration, making it more accessible for Bayesian inference.

### Example: Estimating the Mean of a Normal Distribution

Suppose you want to estimate the mean (μ\mu) of a normal distribution with known variance, based on observed data.

1. **Define the likelihood**: The likelihood is the probability of observing the data D=(x1,x2,…,xn)D = (x_1, x_2, \dots, x_n), given the mean μ\mu and the known variance σ2\sigma^2:
    
    P(D∣μ)=∏i=1n12πσ2exp⁡(−(xi−μ)22σ2)P(D \mid \mu) = \prod_{i=1}^{n} \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left( -\frac{(x_i - \mu)^2}{2\sigma^2} \right)
2. **Specify the prior**: Let's choose a normal prior for μ\mu:
    
    P(μ)∼N(0,10)P(\mu) \sim \mathcal{N}(0, 10)
    
    This means we believe the mean μ\mu is likely to be around 0, with some uncertainty.
    
3. **Compute the posterior**: By applying Bayes’ theorem:
    
    P(μ∣D)∝P(D∣μ)P(μ)P(\mu \mid D) \propto P(D \mid \mu) P(\mu)
    
    This gives us the posterior distribution for μ\mu. However, computing this posterior analytically is difficult, so we use **MCMC** to sample from this distribution.
    
4. **Use MCMC to sample from the posterior**: You can use a package like `rstan` (Stan) or `PyMC3` in Python to perform MCMC sampling. These packages will give you a sample of parameter values from the posterior.
    
5. **Summarize the posterior**: After running MCMC, you get a set of samples for μ\mu. You can compute the posterior mean and credible intervals for μ\mu. For example, you might find:
    
    - **Posterior mean of μ\mu**: μ^=1.3\hat{\mu} = 1.3
    - **95% credible interval**: [1.1,1.5][1.1, 1.5]

### Summary:

To obtain parameters using **Bayesian parameter estimation**:

1. **Specify the likelihood** of the data given the parameters.
2. **Choose a prior** distribution for the parameters.
3. **Compute the posterior distribution** using Bayes’ theorem.
4. **Approximate the posterior** using methods like MCMC or variational inference.
5. **Extract point estimates** (e.g., posterior mean) and **uncertainty** (e.g., credible intervals) from the posterior distribution.

This approach provides both the **point estimates** of the parameters and the **uncertainty** around those estimates, making it a powerful tool for parameter estimation, especially when the model or data is complex.