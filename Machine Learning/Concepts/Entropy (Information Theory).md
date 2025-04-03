# Entropy

[Source](https://medium.com/unpackai/cross-entropy-loss-in-ml-d9f22fc11fe0)
## Definition

In the context of a probability distribution, entropy quantifies the amount of information (or [Bit](Bit.md)s) required to communicate or transmit an outcome from distribution. Formally, it is defined as: $$\mathrm{H}(X)=-\sum_ip(x_i)\log_2p(x_i)$$, where $p(x_i)$ is the probability distribution of each event $x_i$ in the distribution. 

### Interpretation

$\log_2p(x_i)$ measures the amount of "surprise" or uncertainty of the event. If the event is highly likely, its value will be close to 0, indicating little surprise when it happens. Oppositely, if the event is very unlikely, it will be a high value indicting high surprise.

To quantify the total entropy of a distribution $\mathrm{H}(X)$, we take the sum of the surprises of all the events weighted by the probability of them happening. This way events that happen more often contribute more to the total entropy.

The negative sign is to make entropy a positive number.

## Properties of entropy definition

- Non-negative
- Maximized for uniform distribution
	- For a skewed distribution, the entropy will be less because there is little surprise on predicting the next outcome. Example: a really unfair coin with 99% chance of landing on the head.
	- For a uniform distribution, the entropy will be maximized because each outcome is equally likely.
- Additive: the entropy of two independent events is the sum of their entropies.

## Why entropy quantifies bits

- **Why Low Entropy Implies Fewer Bits**: In a low-entropy distribution, fewer bits are needed on average because the dominant events (those with high probabilities) can be communicated with shorter codes. This is the basis of efficient coding strategies like Huffman coding, where shorter codes are assigned to more probable events, minimizing the total bits needed for transmission.
- **Why High Entropy Requires More Bits**: In a high-entropy distribution, where each event is equally probable (like flipping a fair coin), there’s no opportunity for "compression" because each outcome is equally likely. Therefore, we need the maximum number of bits to capture all possibilities.