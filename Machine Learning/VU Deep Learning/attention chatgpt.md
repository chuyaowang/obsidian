# Attention

Self-attention is a sequence-to-sequence mechanism that enables models to process input sequences in parallel while capturing dependencies across different positions.

Unlike recurrent neural networks (RNNs), which process sequences sequentially, self-attention allows for simultaneous computation, leading to improved efficiency and the ability to model long-range dependencies effectively.

## Best of both worlds

Attention mechanisms, particularly **self-attention**, take the "best of both worlds" from Convolutional Neural Networks (CNNs) and Recurrent Neural Networks (RNNs) because they combine the strengths of these architectures while addressing their limitations. Here's a breakdown of why attention achieves this balance:

### From CNNs: Locality and Parallelization

#### Strength of CNNs:

- **Local Feature Extraction**:
    - CNNs excel at learning **localized patterns** (e.g., edges in images or local n-grams in text) through convolutional filters that slide over the input.
- **Parallel Processing**:
    - CNNs process all input elements simultaneously (in parallel) since convolutions can be applied independently across positions.

#### Limitations of CNNs:

- **Fixed Receptive Field**:
    - Standard CNNs struggle to capture **long-range dependencies** because the receptive field is limited unless deeper layers or dilated convolutions are used.
- **Lack of Context Awareness**:
    - While CNNs are good at capturing local patterns, they are less effective in modeling dependencies between distant elements.

#### How Attention Addresses This:

- **Global Context**:
    - Attention mechanisms compute pairwise interactions between all input positions, allowing them to model **global dependencies**.
- **Parallelizable Operations**:
    - Like CNNs, self-attention processes all input elements in parallel, leveraging efficient matrix operations.

---

### From RNNs: Sequential Context and Order Sensitivity

#### Strength of RNNs:

- **Sequential Processing**:
    - RNNs are designed to model **sequential data** by processing inputs in a step-by-step manner, maintaining a hidden state that captures context from previous steps.
- **Order Sensitivity**:
    - RNNs naturally handle the ordering of input data, making them suitable for tasks like time series and natural language processing.

#### Limitations of RNNs:

- **Sequential Bottleneck**:
    - RNNs cannot process inputs in parallel because they depend on the computation of the previous time step's hidden state.
- **Vanishing Gradient Problem**:
    - When modeling long-range dependencies, gradients in RNNs tend to vanish, making it hard to propagate information over long sequences.

#### How Attention Addresses This:

- **Non-Sequential Dependencies**:
    - Self-attention directly computes relationships between all positions in the sequence, bypassing the step-by-step limitation of RNNs.
- **Long-Range Modeling**:
    - Attention mechanisms can easily capture **long-range dependencies** because each position can directly "attend" to any other position, irrespective of their distance in the sequence.

### Attention Combines the Best of Both Worlds

#### Similarities to CNNs:

- **Parallelization**:
    - Like CNNs, attention mechanisms can process the entire input sequence in parallel using matrix multiplications, which is computationally efficient.
- **Scalability**:
    - Self-attention is scalable to large datasets and long sequences because of its parallelization.

#### Similarities to RNNs:

- **Order Sensitivity**:
    - Attention mechanisms can encode order information using **positional encodings**, mimicking the sequential processing capability of RNNs.
- **Context Awareness**:
    - Attention mechanisms capture dependencies across all positions, similar to how RNNs propagate context through hidden states.

### Example: Self-Attention in Transformers

Transformers, powered by self-attention, exemplify this balance:

- They capture both **local and global relationships** (like CNNs) while retaining the ability to model **sequential dependencies** and context (like RNNs).
- By processing inputs in parallel and attending across the entire sequence, they achieve superior performance on tasks like machine translation, text summarization, and image processing.

## Basic Operation of Self-Attention

In self-attention, each output is a weighted sum of all input vectors. The weights are not fixed parameters but are dynamically computed from the inputs themselves. This characteristic ensures that the input and output dimensions remain the same. If a change in dimension is desired, an additional projection layer is required.

The self-attention mechanism can be vectorized by representing the input and output sequences as matrices and performing the operation in three steps:

1. **Compute Compatibility Scores**: Calculate the dot product between each pair of input vectors to assess their similarity.
    
2. **Apply Softmax**: Normalize these scores across each row to obtain the attention weights.
    
3. **Weighted Sum**: Multiply the input vectors by their corresponding attention weights and sum them to produce the output vectors.
    

## Intuition Behind Self-Attention

To understand the effectiveness of self-attention, consider the role of dot products in measuring **similarity**. In recommendation systems, for example, user preferences and item attributes can be represented as vectors. The dot product between these vectors indicates the alignment between user interests and item characteristics. 

Similarly, in self-attention, the dot product between input vectors determines the attention weights, allowing the model to capture relationships between different parts of the input _sequence_.

## Enhancements to Self-Attention

Several modifications enhance the basic self-attention mechanism:

### Scaled Dot-Product Attention

To maintain consistent variance between the input and output of the self-attention operation, the dot product is scaled by the square root of the input dimension. This scaling factor accounts for the increase in vector length with higher dimensions, ensuring numerical stability.

### Key, Query, and Value Vectors

In self-attention, each input vector serves three roles:

- **Query**: The vector used to compute attention weights for the current output.
    
- **Key**: The vector matched against the query to determine the attention weight.
    
- **Value**: The vector that contributes to the final output as part of the weighted sum.
    

To provide flexibility, each input vector is **projected** into three distinct vectors (key, query, and value) using learned parameter matrices. This projection introduces learnable parameters into the self-attention mechanism, enhancing its capacity to model complex relationships.

This adds parameters for self attention layer, which it did not have before. Before it depends on what mechanism generates the embedding vectors.

### Multi-Head Self-Attention

Multi-head attention allows the model to capture different types of relationships by applying _multiple self-attention operations_ in parallel, each focusing on different aspects of the input. The process involves projecting the input sequence into several lower-dimensional spaces, performing self-attention in each space, and then concatenating the results. A final linear transformation integrates these outputs.

### Note

Self attention is fundamentally a set-to-set layer, no access to the sequential structure of the input
## Transformer Architecture

The transformer model is built using transformer blocks, each comprising:

- **Self-Attention Layer**: Propagates information across the sequence.
    
- **Feed-Forward Layer**: Applies a position-wise fully connected network to each token independently.
    
- **Layer Normalization and Residual Connections**: Enhance training stability and convergence.

Notably, self-attention is the sole component that propagates information across the sequence, while other layers operate on each token independently.

## Positional Encoding

Since self-attention is permutation-equivariant, it does not inherently capture the **order** of tokens. To incorporate positional information, positional encodings or embeddings are added to the input vectors. These encodings can be:

- **Learned Positional Embeddings**: Assign a unique embedding to each position in the sequence.
    
- **Fixed Positional Encodings**: Use predefined functions, such as sinusoidal patterns, to encode positions, allowing the model to generalize to longer sequences than those seen during training.

## Causal Self-Attention for Autoregressive Modeling

In tasks like language modeling, where predicting future tokens from past tokens is essential, causal self-attention is employed. This involves masking future tokens during the attention computation to prevent the model from accessing information beyond the current position, ensuring that predictions are based solely on past and present tokens.

## Applications and Impact

Self-attention mechanisms, particularly within transformer architectures, have revolutionized natural language processing by enabling efficient parallel processing and capturing long-range dependencies. They form the foundation of models like BERT and GPT, which have achieved state-of-the-art performance across various tasks, including language translation, sentiment analysis, and text generation.

The scalability and adaptability of self-attention mechanisms continue to drive advancements in deep learning, extending their applicability beyond language processing to areas such as computer vision and reinforcement learning.