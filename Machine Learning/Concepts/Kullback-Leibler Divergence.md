# Kullback-Leibler Divergence

[Medium post for intuitive explanation](https://medium.com/@akp83540/kullback-leibler-divergence-loss-4ddde6132efe)

## Definition

Kullback-Leibler (KL) Divergence Loss is a measure of the difference between two probability distributions. It is widely used in machine learning, particularly for training models that generate or approximate probability distributions. Its mathematical definition is $$D_{KL}(P\|Q)=\sum_{x\in\chi}P(x)\log(\frac{P(x)}{Q(x)})$$, where $P$ is the true distribution and $Q$ is the approximate distribution.

In machine learning, the KL Divergence Loss is often used as the loss function when training generative models, such as Variational Autoencoders (VAEs) or Generative Adversarial Networks (GANs).

## Interpretation

- A KL divergence of 0 means the two distributions are identical, while a higher score indicates the distributions are different.

## Properties

- Scale-invariant
- Does not require any hyperparameters

## Relation to cross entropy

https://stats.stackexchange.com/questions/357963/what-is-the-difference-between-cross-entropy-and-kl-divergence

## KL divergence in comparing substitution matrices

[Probabilistic interpretation of alignment scores](3.%20MIT%20CompBio%20-%20Hashing,%20Database%20Search,%20BLAST%20algorithm.md#Probabilistic%20interpretation%20of%20alignment%20scores)
[Scoring Matrices](3.%20VU%20ASA%20Scoring%20Matrices.md#Scoring%20Matrices)

You can conceptually understand [Entropy (Information Theory)](Entropy%20(Information%20Theory).md) as the amount of surprise of an event. Let's say we're looking at all the possible alignments of A between 2 sequences. If A only aligns with A, then there is no surprise about what aligns with A. So entropy is 0. In contrast, when A has an equal probability of aligning to every other amino acid, the surprise is the highest, and the entropy is the maximum. Formally, entropy is the amount of information needed to communicate the outcome of an event.

Now relative entropy on p91, also called Kullback-Leibler divergence, is a measure of the extra amount of information in the observed distribution of two letters (S_{ij}) compared with the random chance they align together (P_i\*P_j). Notice there is a log in the equation. When the observed distribution is identical to the random distribution, log(1) gives you 0, making the relative entropy 0. In contrast, when the observed distribution is very different from the random distribution, relative entropy would be high. 

To interpret it, when the relative entropy is low, the observed probability of the two letters aligning together is close to random, meaning there is little conservation; when the relative entropy is high, it means the two letters have a high preference of aligning or not aligning together, and this preference is information. So when you sum this over the entire matrix, the total relative entropy tells you how much information on sequence alignment preference this matrix contains. 

For example, blosum62 has higher relative entropy than blosum30 does because it is built from more closely aligned sequences, this tells you more about which amino acids tend to be conserved and which ones can tolerate mutation, whereas for blosum30, since the sequences are more distantly related, their substitution patterns are closer to random, corresponding to low information content.

## Why KL divergence is always positive

The non-negativity of KL divergence is a result of **Gibbs' inequality** and comes from the properties of **relative entropy as a convex function**, not simply from weighting by $p(x)$.

Let's break this down clearly:

1. **KL Divergence and Log Ratio**:
   The KL divergence formula is:
   $$
   D_{\text{KL}}(p \parallel q) = \sum_x p(x) \log \frac{p(x)}{q(x)}
   $$
   This expression can include both positive and negative values of $\log \frac{p(x)}{q(x)}$ depending on whether $p(x)$ is greater than or less than $q(x)$.

2. **Expected Value of Log Ratios**:
   KL divergence can be thought of as the **expected value of the log ratio $\frac{p(x)}{q(x)}$ under the distribution $p(x)$**. Mathematically, this expected value is non-negative because the entire sum can be shown to be an application of **Jensen’s inequality**, which applies here due to the concave nature of the logarithmic function.

3. **Jensen’s Inequality and Convexity**:
   Jensen's inequality states that for a convex function $f$ and a random variable $X$, $\mathbb{E}[f(X)] \geq f(\mathbb{E}[X])$. Since the **negative of the log function** is convex, we get that:
   $$
   \sum_x p(x) \log \frac{p(x)}{q(x)} \geq \log \sum_x p(x) = \log 1 = 0
   $$
   This guarantees that $D_{\text{KL}}(p \parallel q) \geq 0$ with equality only when $p(x) = q(x)$ for all $x$.

4. **Interpretation of Non-Negativity**:
   Intuitively, non-negativity reflects the idea that there is always some amount of "information loss" when approximating one distribution with another, and thus **KL divergence cannot be negative**. The equality $D_{\text{KL}}(p \parallel q) = 0$ only holds when $p(x)$ and $q(x)$ are identical, representing no information loss.

In summary, the **non-negativity of KL divergence** doesn’t come from the fact that $p(x)$ is non-negative alone; rather, it comes from **Jensen’s inequality** applied to the convexity of the log function within the expectation. This property makes $D_{\text{KL}}(p \parallel q) \geq 0$, with zero as its minimum possible value.