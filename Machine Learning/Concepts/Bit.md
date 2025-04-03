# Bit

In the context of information theory, a **bit** (short for "binary digit") is the _basic unit of information_. A bit represents the amount of information required to distinguish between two equally likely outcomes. Mathematically, it corresponds to a choice between two possibilities, such as "0" or "1," "heads" or "tails," etc.

## Bits as Units of Information

When we talk about [Entropy (Information Theory)](Entropy%20(Information%20Theory).md) as being measured in bits, we’re saying that entropy represents the **average number of binary choices (0 or 1)** we would need to uniquely identify the outcome of an event from a probability distribution. This concept is directly tied to how much uncertainty there is in the outcome:

- **1 bit of information** means a simple, single binary choice. For example, the result of a fair coin toss (heads or tails) requires 1 bit to describe, as each outcome is equally likely.
- **Multiple bits** are needed to convey more complex or uncertain outcomes, like identifying a single face from a standard six-sided die roll. Here, more than 1 bit (specifically, about 2.585 bits) would be required on average.

> [!info]- Why 2.585 bits for dice roll
> To understand why more than 1 bit is needed to identify a single face from a standard six-sided die roll, let's consider the nature of bits and the probabilities of outcomes for the die:
> 
> 1. **Bits and Binary Choices**:
>    
>    A bit represents a binary choice (0 or 1), which can distinguish between **two equally likely outcomes**. With 1 bit, we can represent two possible states. For more possible outcomes, we need additional bits:
>    
>    - **1 bit** allows for $2^1 = 2$ possible outcomes.
>    - **2 bits** allow for $2^2 = 4$ possible outcomes.
>    - **3 bits** allow for $2^3 = 8$ possible outcomes.
> 
>    Since a six-sided die has **six outcomes**, 1 or even 2 bits aren't sufficient to encode or identify all six faces because they can only encode 2 and 4 outcomes, respectively.
> 
> 2. **Calculating the Exact Number of Bits Needed (Entropy)**:
>    The entropy for a fair six-sided die, where each face has an equal probability of \( \frac{1}{6} \), is given by:
> 
>    $$
>    H = -\sum_{i=1}^{6} p(x_i) \log_2 p(x_i) = -6 \cdot \frac{1}{6} \log_2 \frac{1}{6} = \log_2 6 \approx 2.585 \text{ bits}
>    $$
> 
>    This value, approximately 2.585 bits, represents the **average number of bits** required to uniquely identify a single face of the die. It’s more than 2 bits because 2 bits only encode up to 4 outcomes, while 3 bits encode up to 8 outcomes (which would be more than necessary).
> 
> 3. **Interpretation of the 2.585 Bits**:
>    Since entropy is an **average measure**, the 2.585 bits indicate the minimum average number of bits required to identify an outcome of a six-sided die roll if we encode it in the most efficient way possible. In practical terms, though, we usually round up to 3 bits, as this allows us to fully capture all six possible outcomes with a little bit of redundancy.

## Why Bits Are Used in Entropy

In the entropy formula $H(X) = - \sum_i p(x_i) \log_2 p(x_i)$, we use the **logarithm base 2** so that entropy is measured in bits. This allows us to interpret entropy as the **expected minimum number of bits** needed to encode or transmit the outcome of an event drawn from the distribution. In practice, this means:

- If we need 1 bit, the distribution is simple (like a fair coin flip).
- Higher entropy values (more bits) indicate more complexity or unpredictability in the distribution, meaning more information is needed to describe the outcomes.

## Example: Encoding Messages

If we were transmitting messages where each message outcome has a probability, entropy tells us how many bits, on average, are necessary to encode these messages efficiently. For a fair coin flip, we need 1 bit because each outcome is equally likely. But if we have a skewed distribution (e.g., a biased coin where heads occurs with a 99% chance), we can encode heads with fewer bits (less information) than tails, because heads is highly predictable. 

## Summary

In this context, a bit is a measure of information that represents the minimal binary choice required to resolve uncertainty in an outcome. When we say entropy is in bits, we mean it represents the average number of such binary choices necessary to identify events from a probability distribution.