# Difference between Inductive and Transductive Graph Learning

The core difference lies in how a model handles unseen data.
## 1. Transductive Learning (Fixed Graph)
In transductive methods (like DeepWalk or PageRank), the model requires the entire graph structure (including the nodes you want to predict) to be present during training.

* The Constraint: If a new node joins the graph, you have to retrain the model from scratch to get an embedding for it.
* The Goal: To "predict" labels for specific, already-known nodes that were unlabeled during training.
* Analogy: Memorizing the specific connections in a fixed seating chart. If a new student arrives, you're lost until you study the new chart.

## 2. Inductive Learning (Generalized Rules)
Inductive methods (like GraphSAGE) learn a generalized rule or function rather than a fixed mapping. They focus on learning how to aggregate information from a neighborhood.

* The Benefit: The model can generate embeddings for nodes it has never seen before, as long as those nodes have features and neighbors the model can "listen" to.
* The Goal: To learn a generalizable heuristic that works on any subgraph or brand-new graph.
* Analogy: Learning the "rules" of how people sit (e.g., "friends sit near friends"). If a new student arrives, you can immediately guess where they belong based on who they talk to.

| Feature | Transductive | Inductive |
|---|---|---|
| New Nodes | Requires retraining | Works instantly (on-the-fly) |
| Graph Context | Global (sees the whole map) | Local (sees neighbors/features) |
| Scalability | Hard for massive/growing data | High; ideal for production systems |
| Common Examples | Node2Vec, DeepWalk, Label Propagation | GraphSAGE, GAT (Graph Attention Networks) |


