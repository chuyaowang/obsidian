# Softmax

The softmax function is a mathematical function that converts a vector of real numbers into a **probability distribution**. It is commonly used in machine learning, especially in the context of multiclass classification problems, to represent the probabilities of different classes.

## Definition

Given a vector $\mathbf{z} = [z_1, z_2, \ldots, z_n]$, the softmax function $\sigma(\mathbf{z})$ is defined as:

$$\sigma(z_i) = \frac{e^{z_i}}{\sum_{j=1}^{n} e^{z_j}}$$

for $i = 1, 2, \ldots, n$.

## Properties

1. **Probability Distribution**: The output of the softmax function is a vector of probabilities that sum to 1.
   
   $\sum_{i=1}^{n} \sigma(z_i) = 1$
   
2. **Exponentiation**: The function uses the exponential function, which ensures that all output values are positive.
3. **Normalization**: Each exponentiated value is divided by the sum of all exponentiated values, normalizing the outputs to sum to 1.

## Example

Consider a vector $\mathbf{z} = [1.0, 2.0, 3.0]$. To compute the softmax of this vector:

1. Compute the exponentials of each element:
   
   $e^{1.0} = 2.7183, \quad e^{2.0} = 7.3891, \quad e^{3.0} = 20.0855$

2. Compute the sum of the exponentials:
   
   $2.7183 + 7.3891 + 20.0855 = 30.1929$

3. Divide each exponential by the sum:
   
   $\sigma(1.0) = \frac{2.7183}{30.1929} \approx 0.0900, \quad \sigma(2.0) = \frac{7.3891}{30.1929} \approx 0.2447, \quad \sigma(3.0) = \frac{20.0855}{30.1929} \approx 0.6652$

So, the softmax output is $\mathbf{\sigma(z)} = [0.0900, 0.2447, 0.6652]$.

## Applications

1. **Multiclass Classification**: In neural networks, especially in the final layer of a [Multiple classification](1.%20VU%20DL%20Introduction.md#Multiple%20classification), softmax is used to convert the logits (raw output values) into probabilities for each class.
2. **Probability Distribution Modeling**: It is used in various probabilistic models where it is necessary to convert a set of scores into a probability distribution.

## Advantages

- **Interpretable Output**: The output probabilities are easy to interpret and can be directly used for decision-making.
- **Differentiability**: The softmax function is differentiable, which makes it suitable for optimization algorithms like gradient descent.

## Derivative

The derivative of the softmax function is often used in the backpropagation algorithm for training neural networks. For a vector $\mathbf{z}$, the derivative with respect to its inputs is:

$\frac{\partial \sigma(z_i)}{\partial z_j} = \sigma(z_i) (\delta_{ij} - \sigma(z_j))$

where $\delta_{ij}$ is the [Kronecker Delta](Kronecker%20Delta.md), which is 1 if $i = j$ and 0 otherwise.

## Computational Stability

In practice, to improve numerical stability, the softmax function is often implemented using the following equivalent formulation:


$\sigma(z_i) = \frac{e^{z_i - \max(\mathbf{z})}}{\sum_{j=1}^{n} e^{z_j - \max(\mathbf{z})}}$

Subtracting the maximum value of the vector $\mathbf{z}$ from each element before exponentiating helps to prevent large exponentials, reducing the risk of [Numerical Overflow](Numerical%20Overflow.md).

## Intuitive Understanding

Intuitively, the softmax function performs a kind of "squashing" operation that takes a vector of real numbers (which could be logits or scores from a model) and transforms it into a vector of probabilities. Here’s how it works and why it makes sense:

### Intuitive Explanation

1. **Exponential Emphasis**:
   - **Highlighting Differences**: By applying the exponential function to each element, the softmax function accentuates the differences between values. Higher values become much larger after exponentiation, while smaller values become comparatively smaller. This emphasizes the _relative importance_ of higher scores.
   
2. **Normalization**:
   - **Sum to One**: The sum of these exponentiated values is computed, and each exponentiated value is then divided by this sum. This ensures that the resulting values form a probability distribution (i.e., they are non-negative and sum to 1).

### Why It Makes Sense

- **Relative Importance**: The original vector might represent some form of raw, unbounded scores indicating the relative importance or likelihood of different classes or outcomes. By exponentiating these scores, we are effectively translating them into a scale where the _differences become more pronounced_.
  
- **Normalization**: Once we have these pronounced differences, normalizing them ensures that they can be interpreted as probabilities. Probabilities inherently need to sum to one, providing a meaningful way to compare the relative likelihoods of different outcomes.
- 
### Why Use Softmax Instead of Other Functions?

- **Exponentiation and Differentiation**: The exponential function’s properties ensure that even _small differences in scores become significant after exponentiation_, which is crucial for distinguishing between classes. Moreover, the softmax function is differentiable, allowing it to be used effectively in gradient-based optimization methods common in neural networks.
  
- **Handling Logits**: Raw scores (logits) can be negative, zero, or positive, and their scale can vary. The softmax function handles this by converting any range of input values into a well-defined probability distribution.

## Temperature

The temperature parameter in the softmax function is a scaling factor that can be used to **control the "sharpness" or "smoothness" of the resulting probability distribution**. This parameter is often denoted by $T$.

### Temperature in Softmax Function

The standard softmax function for a vector $\mathbf{z}$is:

$\sigma(z_i) = \frac{e^{z_i}}{\sum_{j=1}^{n} e^{z_j}}$

Introducing a temperature parameter $T$, the modified softmax function becomes:

$\sigma_T(z_i) = \frac{e^{z_i / T}}{\sum_{j=1}^{n} e^{z_j / T}}$

### Effects of the Temperature Parameter

1. **High Temperature ( $T > 1$)**:
   - When the temperature $T$ is greater than 1, the softmax function produces a smoother, more uniform probability distribution. This means that the differences between the probabilities of different outcomes are reduced, making the distribution more "soft".
   - For example, if $T$ is very high, the softmax function approaches a uniform distribution where all probabilities are almost equal.

2. **Low Temperature ( $0 < T < 1$)**:
   - When the temperature $T$ is less than 1, the softmax function produces a sharper, more peaked probability distribution. This means that the differences between the probabilities of different outcomes are accentuated, making the distribution more "hard".
   - For example, if $T$ is very low, the softmax function approaches a one-hot encoding where the highest value dominates the probability distribution, and other values have probabilities close to zero.

### Why Use Temperature?

1. **Control Exploration and Exploitation**:
   - In reinforcement learning and some probabilistic models, the temperature parameter is used to control the trade-off between exploration (trying out less likely actions) and exploitation (choosing the most likely action). A higher temperature promotes exploration, while a lower temperature promotes exploitation.

2. **Adjust Sensitivity**:
   - Temperature can be used to adjust the sensitivity of the softmax function to the differences in the input values. In neural networks, for example, temperature scaling can be used during inference to control the confidence of the predictions.

3. **Smooth vs. Sharp Decisions**:
   - When modeling probabilistic decisions, temperature can help in smoothing out the decision boundaries or making them sharper, depending on the application needs.

### Example

Consider the vector $\mathbf{z} = [1.0, 2.0, 3.0]$:

- **Standard Softmax ( $T = 1$)**:
  $\sigma(1.0) = \frac{e^1}{e^1 + e^2 + e^3} \approx 0.090, \quad \sigma(2.0) = \frac{e^2}{e^1 + e^2 + e^3} \approx 0.245, \quad \sigma(3.0) = \frac{e^3}{e^1 + e^2 + e^3} \approx 0.665$

- **High Temperature ( $T = 2$)**:
  $\sigma_T(1.0) = \frac{e^{1/2}}{e^{1/2} + e^{2/2} + e^{3/2}} \approx 0.211, \quad \sigma_T(2.0) = \frac{e^{2/2}}{e^{1/2} + e^{2/2} + e^{3/2}} \approx 0.307, \quad \sigma_T(3.0) = \frac{e^{3/2}}{e^{1/2} + e^{2/2} + e^{3/2}} \approx 0.482$

- **Low Temperature ( $T = 0.5$)**:
  $\sigma_T(1.0) = \frac{e^{1/0.5}}{e^{1/0.5} + e^{2/0.5} + e^{3/0.5}} \approx 0.019, \quad \sigma_T(2.0) = \frac{e^{2/0.5}}{e^{1/0.5} + e^{2/0.5} + e^{3/0.5}} \approx 0.119, \quad \sigma_T(3.0) = \frac{e^{3/0.5}}{e^{1/0.5} + e^{2/0.5} + e^{3/0.5}} \approx 0.861$

As seen, with $T = 2$, the probabilities are more uniform, while with $T = 0.5$, the probabilities are more skewed towards the highest value.

In summary, the temperature parameter in the softmax function is a powerful tool to control the spread of the resulting probability distribution, allowing it to be adjusted from very smooth to very sharp depending on the application requirements.

## Derivative of softmax

[Derivative of softmax and cross entropy 1](https://towardsdatascience.com/derivative-of-the-softmax-function-and-the-categorical-cross-entropy-loss-ffceefc081d1)
[Derivative of softmax and cross entropy 2](https://levelup.gitconnected.com/killer-combo-softmax-and-cross-entropy-5907442f60ba)

[YouTube step by step](https://www.youtube.com/watch?v=M59JElEPgIg)
$$
\begin{aligned}
\frac{\partial y_i}{\partial o_j} &= \frac{\partial\frac{\exp{o_i}}{\sum_j\exp{o_j}}}{\partial o_j}\\
&=\frac{\frac{\partial}{\partial o_j}\exp{o_i}\sum_j{\exp{o_j}}-\exp{o_i}\frac{\partial}{\partial o_j}\sum_j{\exp{o_j}}}{(\sum_j{\exp{o_j}})^2}
\end{aligned}
$$when $i=j$:$$
\begin{aligned}
\frac{\partial y_i}{\partial o_j} &= \frac{\exp{o_i}\sum_j{\exp{o_j}}-\exp{o_i}\exp{o_j}}{(\sum_j{\exp{o_j}})^2}\\
&=\frac{\exp{o_i}(\sum_j{\exp{o_j}}-\exp{o_j})}{(\sum_j{\exp{o_j}})^2}\\
&=\frac{\exp{o_i}}{\sum_j{\exp{o_j}}}\cdot\frac{\sum_j{\exp{o_j}}-\exp{o_j}}{\sum_j{\exp{o_j}}}\\
&=y_i(1-y_j)
\end{aligned}
$$when $i\neq j$:$$
\begin{aligned}
\frac{\partial y_i}{\partial o_j} &= \frac{0\cdot\sum_j{\exp{o_j}}-\exp{o_i}\exp{o_j}}{(\sum_j{\exp{o_j}})^2}\\
&=\frac{\exp{o_i}}{\sum_j{\exp{o_j}}}\cdot\frac{-\exp{o_j}}{\sum_j{\exp{o_j}}}\\
&=-y_iy_j
\end{aligned}
$$ or $$
\frac{\partial y_i}{\partial o_j} = y_i(\delta_{ij}-y_j)
$$, where $\delta_{ij}$ is the Kronecker delta function which is 1 when $i=j$ and 0 otherwise.

## Log-sum-exp trick

[Explanation](https://gregorygundersen.com/blog/2020/02/09/log-sum-exp/)

Instead of the original definition, compute `exp(x-logsumexp(x))`, which is equivalent to softmax but more numerically stable.