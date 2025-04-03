#### Question 1 (0.5 pt)

  

ANSWER:

For a given $x$, the encoder with parameters $\theta$ outputs the $\mu_\theta(x)$ and $\log\sigma^2_\theta(x)$ that define the variational posterior $q_\theta(z|x)$, which we assume to be a Gaussian with mean $\mu_\theta$ and variance $\sigma_\theta^2$.

Sampling directly from this distribution does not allow computing the gradient $\frac{\partial z}{\partial \theta}$ for back-propagation. The reparameterization trick instead samples using the function $$z = \mu_\theta(x) + \sigma_\theta(x)\odot\epsilon$$, where $\epsilon$ is sampled from a normal distribution with mean 0 and variance 1. Since $\epsilon$ does not depend on $\theta$, when computing the gradient $\frac{\partial z}{\partial \theta}$, it can be treated as a constant. This way $\frac{\partial z}{\partial \theta}$ can be calculated, and the randomness in the sampling process does not affect the calculation.