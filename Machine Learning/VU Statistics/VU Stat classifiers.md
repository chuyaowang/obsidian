# Classifiers


## Logistic regression

2 class classification
$$
\theta(x) = \frac{1}{1+e^{-(\beta_0+\beta_1x)}} 
$$

## Bayesian classifier


By definition

$$p(M|L) = \frac{p(M,L)}{p(L)}$$

and

$$p(S|M,L) = \frac{p(L,M,S)}{p(M,L)}$$

From which we get

$$p(L,M,S) = p(S|M,L) \cdot p(M|L) \cdot p(L)$$

Also, by definition

$$p(L|M,S) = \frac{p(L,M,S)}{p(M,S)}$$

By substitution we obtain:

### Bayes rule for joint distributions

$$p(L|M,S) = \frac{p(S|M,L) \cdot p(M|L) \cdot p(L)}{p(M,S)}$$

But how can we estimate $p(S|M,L)$?

Use the naive assumption that M and S are conditionally independent!

$$
p(L|M,S) = \frac{p(S|L)\cdot p(M|L)\cdot p(L)}{p(M,S)}
$$
