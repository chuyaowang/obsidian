# Cross-Entropy Loss

The cross-entropy loss function is based on [Entropy (Information Theory)](Entropy%20(Information%20Theory).md), and it measures the "distance" or difference between two probability distributions. It’s commonly used in [Binary and multiple classification](1.%20VU%20DL%20Introduction.md#Binary%20classification) problems to evaluate how well a model's predicted probability distribution aligns with the true distribution of labels.

## Understanding Cross-Entropy and Its Relation to Entropy

1. **Entropy of the True Distribution**:
   If we consider the true distribution of labels $p$, the entropy $H(p)$ is a measure of the inherent uncertainty in this distribution. For example, in a binary classification problem where $p = [0.5, 0.5]$, entropy measures the uncertainty associated with predicting either class. For a ground-truth distribution $p(y)$ over all classes $y$, the entropy $H(p)$ is defined as:

   $$
   H(p) = - \sum_{y} p(y) \log p(y)
   $$

2. **Cross-Entropy Between True and Predicted Distributions**:
   The cross-entropy $H(p, q)$ measures the "cost" or "penalty" of using a predicted probability distribution $q$ to represent the true distribution $p$. Cross-entropy tells us how many bits are needed, on average, to encode the true labels using the model’s predicted distribution. For a true distribution $p(y)$ and a predicted distribution $q(y)$, the cross-entropy $H(p, q)$ is defined as:

   $$
   H(p, q) = - \sum_{y} p(y) \log q(y)
   $$

   Notice that while entropy only involves $p(y) \log p(y)$, cross-entropy ==replaces the log term with $\log q(y)$==, reflecting how "off" the predictions are from the true distribution.

3. **Interpreting Cross-Entropy as a Loss Function**:
   In classification, the ground-truth distribution $p(y)$ is typically a one-hot vector, where the probability of the correct class is 1, and all other classes are 0. For instance, if the true class is $y = 1$, then $p = [0, 1, 0, \dots, 0]$. In this case, cross-entropy simplifies to:

   $$
   H(p, q) = - \log q(y_{\text{true}})
   $$

   Here, $q(y_{\text{true}})$ is the model’s predicted probability for the correct class. The cross-entropy loss penalizes incorrect predictions by assigning a high loss value when $q(y_{\text{true}})$ is low (i.e., when the model is less confident about the correct class). Conversely, if the model assigns a high probability to the correct class, $-\log q(y_{\text{true}})$ becomes small, reducing the loss.

4. **Why Cross-Entropy Loss Works Well**:
   Cross-entropy loss is effective because it not only evaluates whether the model correctly classifies an instance but also penalizes the model based on its confidence in the prediction. This encourages the model to assign high probabilities to the correct classes, thereby improving the overall probability calibration.

5. **Relationship to Kullback-Leibler (KL) Divergence**:
   Cross-entropy can also be understood in terms of [Kullback-Leibler Divergence](Kullback-Leibler%20Divergence.md), which measures how much one probability distribution diverges from another. Specifically, the KL divergence $D_{\text{KL}}(p \parallel q)$ between the true distribution $p$ and the predicted distribution $q$ is given by:

   $$
   D_{\text{KL}}(p \parallel q) = H(p, q) - H(p)
   $$

   Since $H(p)$ is constant for a given true distribution, minimizing the cross-entropy $H(p, q)$ is equivalent to minimizing the KL divergence. This means cross-entropy loss minimizes the difference between the predicted and true distributions, effectively aligning the model’s predictions with the ground-truth labels.

## Why log(q(y)) reflects model confidence

The term $\log(q(y))$ in the cross-entropy loss function reflects the **confidence** of the model in predicting the true label and thus indicates how "off" or "incorrect" the prediction is relative to the true distribution. Here's why:

1. **The Meaning of $\log(q(y))$**:
   When $q(y)$ represents the predicted probability of the true class $y$, the logarithm $\log(q(y))$ measures the "surprise" or "uncertainty" associated with this prediction:
   - If $q(y)$ is high (close to 1), then $\log(q(y))$ is closer to zero. This means the model is confident about the correct class, resulting in a lower penalty in the loss function.
   - If $q(y)$ is low (close to 0), then $\log(q(y))$ is a large negative number, resulting in a higher penalty. This reflects that the model assigned a low probability to the correct class, indicating a poor prediction.

2. **Logarithmic Sensitivity**:
   The logarithmic function is sensitive to values close to zero, which means that **incorrect predictions** (where $q(y)$ is low) lead to a significantly larger penalty than predictions that are nearly correct. This effectively pushes the model to allocate high probabilities to the correct classes and to avoid low-probability assignments to correct labels.

3. **Relationship to Model Confidence**:
   Since $q(y)$ represents the probability the model assigns to the correct class:
   - A model that’s highly confident and correct will have $q(y) \approx 1$, leading to a low $-\log(q(y))$.
   - A model that’s uncertain or incorrect will assign $q(y)$ a value much less than 1, leading to a high $-\log(q(y))$. This penalizes the model, as the high cross-entropy loss signals a large divergence from the true distribution.

4. **Why This Reflects "Offness"**:
   The cross-entropy loss sums up $-\log(q(y))$ across all samples, effectively capturing the **average difference** between the predicted probabilities and the true probabilities. Since the logarithmic scale amplifies small probabilities, the cross-entropy emphasizes cases where the model is very wrong (i.e., it assigns a low probability to the true class). This gradient provides the model with feedback to adjust and produce higher probabilities for correct predictions.

## Derivative of the cross entropy loss

[Derivative of softmax](Softmax.md#Derivative%20of%20softmax)
[Derivative of softmax and cross entropy 1](https://towardsdatascience.com/derivative-of-the-softmax-function-and-the-categorical-cross-entropy-loss-ffceefc081d1)
[Derivative of softmax and cross entropy 2](https://levelup.gitconnected.com/killer-combo-softmax-and-cross-entropy-5907442f60ba)
