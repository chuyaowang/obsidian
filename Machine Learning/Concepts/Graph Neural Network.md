# Graph Neural Network Explained: Summary of Different Graph Embedding Methods

[Graph neural nets explained](https://medium.com/@ManishChablani/graph-neural-nets-explained-summary-of-different-graph-embedding-methods-8fd15778a490)

Graph neural nets are used to generate embeddings for graphs. They learn the patterns of the graph to generate meaningful embeddings for downstream ML tasks.
## Node2Vec

Generates [Node Embeddings](Graph%20Embedding.md#Node%20Embeddings) in word2vec style. It has been mostly replaced by more recent methods.

The advantage is fast. However, node type and relationship type are not considered when generating embeddings.

## Graph Neural Networks

GNNs operate naturally on graph type data. By extracting and utilizing features from the underlying graph, GNNs can make more informed predictions about entities in these interactions.

Modern popular GNN algorithms:
- Graph Convolutional Networks (GCN)
- Graph Attention Networks (GAT)
- Graph Sample and Aggregate (GraphSAGE)
- Graph Isomorphism Network (GIN)

GNNs are divided into two approaches: [Inductive and Transductive Learning](Inductive%20and%20Transductive%20Learning.md). In short, transductive learning studies a fixed graph. New predictions are made in the same graph. Inductive learning learns to generalize to new graphs.

## GraphSAGE

[Paper](https://arxiv.org/abs/1706.02216)

A inductive framework that leverages node **feature information** (eg. text attributes) generate [Node Embeddings](Graph%20Embedding.md#Node%20Embeddings). The basic idea of node embedding is to use dimensionality reduction techniques to distill the high-dimensional information about a node’s graph neighborhood into a dense vector embedding.

Convolution operators are useful for generating node embeddings. Prior to GraphSAGE, GCNs have only been applied with transductive approach. GraphSAGE extends it to inductive learning and uses trainable aggregation functions instead of simple convolutions.

Instead of training an embedding vector for each node, a set of **aggregator functions** are trained to aggregate feature information from a node's local neighborhood. The aggregator functions reach different search depths (number of hops) away from the given node.

In the training process, close nodes are trained to have similar representations, while distant nodes have dissimilar representations.

Once the model parameters are trained. The model generates embeddings for each node.

## PinSage

[Paper](https://arxiv.org/pdf/1806.01973.pdf)

An improvement over GraphSAGE that work for production-level data. Instead of global, PinSage does local convolution in the neighborhood of the node. A local random walk is used to sample the neighborhood. This improves performance over random sampling. By counting the number of times visited in the random walk, the neighborhood nodes are ranked in their importance to the center node.