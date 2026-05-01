# F1 Score, AUC, PR AUC Scores

These three metrics are fundamental for evaluating classification models, especially when dealing with imbalanced data (like your edge prediction task, where there are far more "False" edges than "True" edges).

Here is a breakdown of what they are and how to interpret them:

### 1. F1 Score

The F1 Score is the harmonic mean of **Precision** and **Recall**. It evaluates a model's performance using a _specific, hard threshold_ (e.g., checking if a prediction is `>= 0.5` or `>= your_dynamic_threshold`).

To understand F1, you must understand its two halves:

- **Precision:** _"Out of all the edges the model predicted as True, how many were actually True?"_ (High precision means very few False Positives).
- **Recall:** _"Out of all the actual True edges in the graph, how many did the model successfully find?"_ (High recall means very few False Negatives).

**How to interpret it:**

- **Scale:** 0.0 (worst) to 1.0 (perfect).
- **Meaning:** An F1 score of 1.0 means your model has perfect precision and perfect recall at your chosen threshold. It is a strict metric; if a model predicts 1000 False Positives just to find 10 True Positives, its Recall is 100%, but its Precision drops to near 0%, dragging the F1 Score down with it.

### 2. AUC (ROC AUC)

**AUC** stands for _Area Under the Receiver Operating Characteristic Curve_. Unlike the F1 score, AUC does _not_ rely on a single threshold like `0.5`. Instead, it evaluates the model's raw probabilities across **all possible thresholds**.

Mathematically, it represents the probability that the model will rank a randomly chosen True edge higher than a randomly chosen False edge.

**How to interpret it:**

- **0.5:** Your model is guessing randomly (a coin flip).
- **1.0:** Perfect ranking. Every single True edge was given a higher probability than every single False edge.
- **Meaning:** ROC AUC is fantastic for checking if your model is fundamentally "learning" the visual features. However, **it can be overly optimistic on highly imbalanced data**. Because it factors in True Negatives, correctly identifying 10,000 obvious dead edges can artificially inflate the score, hiding the fact that the model is struggling with the minority positive class.

### 3. PR AUC (Average Precision)

**PR AUC** stands for _Precision-Recall Area Under the Curve_. Like ROC AUC, it evaluates the model across _all possible thresholds_, but it plots Precision against Recall instead of True Positive Rate against False Positive Rate.

**This is the gold standard metric for highly imbalanced datasets.** It completely ignores True Negatives and focuses entirely on the minority class (the True edges).

**How to interpret it:**

- **Baseline (Random Guessing):** Unlike ROC AUC where random is 0.5, the baseline for PR AUC is the percentage of True edges in your dataset. If only 2% of your edges are True, a random model will get a PR AUC of `0.02`.
- **1.0:** Perfect ranking with zero False Positives at any recall level.
- **Meaning:** If your ROC AUC is `0.95` but your PR AUC is `0.30`, it means your model ranks things generally well, but the moment it tries to find the very hard True edges, it accidentally triggers an avalanche of False Positives. If your PR AUC is high (e.g., `0.85+` on a 2% baseline), you have an exceptional, production-ready model.

### Summary for your specific use case:

- Use **ROC AUC** to verify the neural network is learning and gradients are healthy.
- Use **PR AUC** to see the _true_ performance of the model on the sparse graph.
- Use **F1 Score** to prove that your dynamic threshold script successfully extracted the best possible Yes/No predictions out of the model's raw probabilities.