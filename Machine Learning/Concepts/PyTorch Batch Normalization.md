# Batch Normalization

## The Problem it Solves

Imagine you just concatenated two features for a node:

- Feature A: The raw pixel intensity (values around `0.1` to `1.0`).
- Feature B: A deep network embedding (values around `-50.0` to `50.0`).

If you pass this directly into the next neural network layer, the weights attached to Feature B will completely overpower Feature A. Batch Normalization fixes this by standardizing every feature across the current batch.

## How it Calculates Normalization (The Math)

When a batch of data (e.g., 1000 nodes, each with 80 features) passes through the layer during training, `BatchNorm1d` does the following **for each of the 80 features independently**:

**Step 1: Calculate the Batch Mean ($\mu$) and Variance ($\sigma^2$)** It looks at the current batch of 1000 nodes and calculates the average value and the variance for Feature 1, Feature 2, etc.

**Step 2: Normalize the Data** It takes every individual node's feature and standardizes it using the formula: $$x_{normalized} = \frac{x - \mu}{\sqrt{\sigma^2 + \epsilon}}$$ _(Note: $\epsilon$ is a tiny number like $1e-5$ added to the variance to prevent dividing by zero if all values are identical)._ At this exact moment, every feature now has a mean of `0.0` and a standard deviation of `1.0`.

**Step 3: Scale and Shift (The Learnable Part)** If the network is forced to keep everything strictly at mean 0 and variance 1, it actually limits the network's expressive power. So, BatchNorm applies a final linear transformation using two **learnable parameters** per feature:

- $\gamma$ (Gamma): A scaling factor (initialized to 1).
- $\beta$ (Beta): A shifting factor (initialized to 0).

$$y = \gamma * x_{normalized} + \beta$$

During backpropagation, the optimizer adjusts $\gamma$ and $\beta$. This allows the network to learn the _perfect optimal distribution_ for that specific feature.

---

## The Crucial Difference: Training vs. Testing

Batch Normalization behaves completely differently depending on whether your model is in `model.train()` mode or `model.eval()` mode.

**During Training (`model.train()`):**

- It normalizes the data using the mean and variance of the _current live batch_.
- **Running Statistics:** In the background, it keeps a running tally (an exponential moving average) of the mean and variance across all the batches it has ever seen.

**During Testing/Inference (`model.eval()`):**

- It **stops** looking at the current batch.
- If you pass a single graph to the model during testing, it can't calculate a reliable batch mean anyway. So, it uses the **Running Statistics** it accumulated during training to perform the normalization.
- This ensures that your model behaves deterministically. If you pass the exact same node into the model twice, you will get the exact same output, regardless of what other nodes are in the batch with it.

By applying this right after your skip connections, you are ensuring that your raw pixel data and your deep GNN embeddings are perfectly leveled out and scaled before the next set of weights looks at them!