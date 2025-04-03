# Bias Variance Trade-off

## Bias and Variance in Machine Learning Models

Bias and variance are two fundamental sources of error that affect a machine learning model’s performance. Understanding their trade-off is essential for building models that generalize well to unseen data.

---

## Bias

Bias refers to the error introduced by approximating a real-world problem with a simplified model. It measures how much the model's predictions **systematically deviate** from the true values.

### Characteristics of High-Bias Models

- Make strong assumptions about the data.
- Tend to **underfit** the training data (fail to capture patterns).
- Have limited flexibility.
- Examples: Linear regression, simple decision trees, Naïve Bayes.

### Mathematical Perspective

For a given dataset with true function $f(x)$, model predictions $\hat{f}(x)$, and expected value $E[\hat{f}(x)]$, bias is:

$$Bias^2 = \left( E[\hat{f}(x)] - f(x) \right)^2$$

A high-bias model consistently predicts values far from the actual target.

---

## Variance

Variance refers to the model’s sensitivity to fluctuations in the training data. It quantifies how much the model’s predictions would change if different training datasets were used.

### Characteristics of High-Variance Models

- Capture noise in the training data.
- Tend to **overfit** (memorize training data but fail on new data).
- Have high model complexity.
- Examples: Deep neural networks, complex decision trees.

### Mathematical Perspective

Variance measures the spread of model predictions around their expected value:

$$Variance = E\left[\left( \hat{f}(x) - E[\hat{f}(x)] \right)^2\right]$$

A high-variance model produces predictions that fluctuate significantly for different training sets.

---

## Bias-Variance Trade-off

The total error of a model is the sum of bias, variance, and irreducible noise:

$$Error = Bias^2 + Variance + \sigma^2$$

where:

- $Bias^2$ captures systematic error due to incorrect model assumptions.
- $Variance$ captures sensitivity to training data changes.
- $\sigma^2$ is the **irreducible error** (inherent noise in the data).

### Trade-off Explained

- **Low Bias, High Variance** → The model learns too much from training data, leading to overfitting.
- **High Bias, Low Variance** → The model is too simplistic and generalizes poorly, leading to underfitting.
- **Optimal Balance** → The model achieves a **trade-off** where both bias and variance are minimized, leading to the best generalization.

**Graphically**, the trade-off can be seen as:

📉 **Bias decreases** → Model becomes more flexible but may overfit.  
📈 **Variance increases** → Model becomes sensitive to training data fluctuations.

---

## How Bagging Helps Reduce Variance

- Decision trees are high-variance models; they can fit training data very well but may overfit.
- [Bagging](9.%20VU%20BDA%20Random%20Forest.md#Bagging) (Bootstrap Aggregating) creates multiple decision trees on different samples and averages their predictions.
- Since variance is reduced by averaging multiple models:

$$Var\left(\frac{1}{B} \sum_{i=1}^{B} \hat{f}_i(x) \right) = \frac{1}{B} Var(\hat{f}(x))
$$
- **Bias remains nearly the same**, but variance decreases, leading to better generalization.

---

## Models

|Model Type|Bias|Variance|Generalization|
|---|---|---|---|
|**Linear Regression**|High|Low|Poor if data is complex|
|**Decision Trees**|Low|High|Overfits if deep|
|**Random Forest (Bagging Trees)**|Low|Low|Good generalization|
|**Deep Neural Networks**|Very Low|Very High|Overfits without regularization|
