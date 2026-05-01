# The Mathematics of Prompt Caching in LLMs

[blog link](https://ngrok.com/blog/prompt-caching)

Prompt caching allows developers to achieve significant cost and latency reductions (up to 10x cheaper and 85% faster for long prompts). But what exactly is being cached? The answer lies in the matrix mathematics of the Transformer's Attention mechanism.

Here is a breakdown of the mathematical process described in the ngrok engineering blog.

## 1. From Tokens to Embeddings

Before any complex math occurs, text is chopped up by a **Tokenizer** into integer IDs (tokens). Because mathematical functions require vectors, not plain integers, these tokens are converted into **Embeddings**.

An embedding is an array of length $n$ representing a position in an $n$-dimensional space (e.g., $n > 10,000$ in modern models).

$$\text{Tokens (1D Array)} \rightarrow \text{Embeddings (Matrix of } T \times n)$$

_(Where_ $T$ _is the number of tokens and_ $n$ _is the number of dimensions)._

Positional data is also encoded into these matrices so the LLM respects the sequence of the prompt.

## 2. The Attention Mechanism: Mixing Meaning

The actual caching takes place in the **Attention mechanism** of the Transformer block. The goal of attention is to help the LLM understand the relationships between tokens by taking an input matrix of embeddings and combining them in a weighted fashion.

### The Core Matrices: $W_Q, W_K, W_V$

During training, the model learns three specific $n \times n$ weight matrices:

- $W_Q$: Query weights
    
- $W_K$: Key weights
    
- $W_V$: Value weights
    

During standard inference, the model multiplies the input embedding matrix by these learned weights to derive three new matrices: $Q$ (Query), $K$ (Key), and $V$ (Value).

$$Q = \text{Embeddings} \times W_Q$$$$K = \text{Embeddings} \times W_K$$$$V = \text{Embeddings} \times W_V$$

### Calculating Attention Weights

To determine how much focus (or "attention") a token should give to other tokens, the model multiplies $Q$ by the transpose of $K$. This produces the **attention weights**, dictating the relevance of tokens to one another.

$$\text{Weights} = Q \times K^T$$

_(Note: Softmax scaling is applied to these weights, though simplified in the conceptual explanation)._

Finally, these weights are multiplied by the Value matrix ($V$) to determine which semantic dimensions to carry forward to the next stage of the network:

$$\text{Output} = \text{Weights} \times V$$

## 3. The Problem: Redundant Matrix Multiplication

LLMs generate text **autoregressively** (one token at a time). In a naive inference loop, when the LLM appends a newly generated token to the prompt and runs the sequence again, it re-calculates $Q$, $K$, and $V$ for _every single token_ in the prompt.

For a prompt like "Mary had a little...", processing the word "little" forces the model to recalculate the exact same attention weights for "Mary", "had", and "a" over and over again.

## 4. The Mathematical Solution: KV Caching (Prompt Caching)

Prompt caching eliminates these redundant calculations by making two fundamental changes to the inference loop:

1. **Only feed the newest token** into the model, rather than the entire prompt array.
    
2. **Cache the** $K$ **and** $V$ **matrices** from previous iterations.
    

### The Caching Math in Action

When a new token arrives, the model only performs matrix multiplication for that specific token:

**Step 1: Calculate** $Q$**,** $K$**, and** $V$ **for the** _**new**_ **token only (resulting in** $1 \times n$ **matrices):**

$$Q_{new} = \text{Embedding}_{new} \times W_Q$$$$K_{new} = \text{Embedding}_{new} \times W_K$$$$V_{new} = \text{Embedding}_{new} \times W_V$$

**Step 2: Append the new Key and Value rows to the cached matrices:**

$$K_{total} = \text{Append}(K_{cached}, K_{new})$$$$V_{total} = \text{Append}(V_{cached}, V_{new})$$

**Step 3: Calculate the new weights and output using the cached data:**

$$\text{New Scores} = Q_{new} \times K_{total}^T$$$$\text{New Output} = \text{New Scores} \times V_{total}$$

### Summary

By caching the Keys ($K$) and Values ($V$) computed during the processing of the prompt, the provider's GPUs can skip massive $T \times n$ matrix multiplications. When you use prompt caching, the API provider stores these exact 1s and 0s (the $K$ and $V$ matrices for your prompt's tokens) in memory. When you send the same prompt again, the math picks up exactly where it left off, resulting in massive computational—and financial—savings.