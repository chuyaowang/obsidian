# Inductive and transductive learning

In the context of [Graph Neural Networks](Graph%20Neural%20Network.md) (GNNs), the terms "inductive" and "transductive" refer to different approaches to learning and inference on graph-structured data. Here’s a detailed explanation of the differences between these two paradigms:

### Transductive Learning

**Definition**: In transductive learning, the model is trained and tested on the same fixed graph. The nodes and their connections used during training are the same nodes and connections used during inference. The model does not generalize to unseen nodes or graphs but rather focuses on predicting labels for the nodes within the given graph.

**Characteristics**:
1. **Fixed Graph**: The entire graph structure is known and remains fixed during both training and inference.
2. **Node Embeddings**: Node embeddings are learned for specific nodes within the given graph. These embeddings are not generalized to unseen nodes or graphs.
3. **Examples**: 
   - **Graph Convolutional Network (GCN)**: GCNs are typically used in a transductive manner where the graph and all its nodes are present during training.
   - **Label Propagation**: Another example where the model propagates labels through a fixed graph.

**Applications**:
- **Semi-Supervised Node Classification**: Predicting labels for nodes within a known graph where some nodes have labels, and others do not.
- **Link Prediction**: Predicting the existence of edges within the same graph used during training.

### Inductive Learning

**Definition**: In inductive learning, the model is trained on one set of graphs or subgraphs and is capable of generalizing to new, unseen graphs or nodes during inference. The model learns a general function that can be applied to any graph structure, not just the ones seen during training.

**Characteristics**:
1. **Generalization**: The model generalizes to new nodes and graphs not present during training.
2. **Node Embeddings**: Node embeddings are computed on-the-fly based on the learned function, making the model adaptable to new nodes and graphs.
3. **Examples**:
   - **GraphSAGE (Graph Sample and Aggregation)**: GraphSAGE generates node embeddings by sampling and aggregating features from a node’s neighborhood, allowing it to generalize to unseen nodes and graphs.
   - **GIN (Graph Isomorphism Network)**: Another GNN that can be used in an inductive setting.

**Applications**:
- **Node Classification**: Predicting labels for nodes in previously unseen graphs.
- **Graph Classification**: Classifying entire graphs, where each graph is treated as a separate instance, and the model must generalize to new graphs.
- **Dynamic Graphs**: Handling graphs that evolve over time, where new nodes and edges can appear.

### Key Differences

| Aspect                  | Transductive Learning                   | Inductive Learning                       |
|-------------------------|-----------------------------------------|------------------------------------------|
| **Graph Scope**         | Fixed graph during training and testing | Generalizes to unseen nodes/graphs       |
| **Node Embeddings**     | Learned for specific nodes in the graph | Computed on-the-fly for new nodes        |
| **Model Flexibility**   | Limited to the training graph           | Adaptable to new graph structures        |
| **Training Data**       | Entire graph used for training          | Trained on subsets or multiple graphs    |
| **Inference**           | Only on nodes within the training graph | On new nodes or entirely new graphs      |
| **Examples**            | GCN, Label Propagation                  | GraphSAGE, GIN, Graph Attention Networks |

### Example Use Cases

1. **Transductive Learning**:
   - **Social Networks**: Classifying users in a social network where the network structure is fixed and fully known.
   - **Citation Networks**: Predicting the subject area of papers in a citation network where all the papers and citations are known.

2. **Inductive Learning**:
   - **Biological Networks**: Predicting functions of proteins where new proteins and their interactions are continuously discovered.
   - **Recommendation Systems**: Providing recommendations to new users or for new items in a dynamic user-item interaction graph.

### Summary

Transductive learning GNNs focus on tasks within a fixed graph, making them suitable for applications where the graph does not change over time. Inductive learning GNNs, on the other hand, are designed to generalize to new, unseen graphs or nodes, making them more versatile and applicable to dynamic or evolving graphs. Understanding these differences is crucial for selecting the appropriate GNN approach based on the specific requirements and nature of the graph data.