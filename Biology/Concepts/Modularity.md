# Modularity

**Modularity** is a measure used in network analysis to quantify the strength of the division of a network into communities (or modules). It evaluates the _density of links inside_ communities compared to _links between_ communities. High modularity indicates a structure where there are many edges within communities and comparatively fewer edges between them.

## Mathematical Definition

Modularity $Q$is defined as:

$$Q = \frac{1}{2m} \sum_{i,j} \left[ A_{ij} - \frac{k_i k_j}{2m} \right] \delta(c_i, c_j)$$

where:
- $A_{ij}$ is the weight of the edge between node $i$ and node $j$. For unweighted networks, this is simply 1 if there is an edge and 0 otherwise.
- $k_i$ and $k_j$ are the degrees of nodes $i$ and $j$, respectively (i.e., the number of edges connected to $i$and $j$.
- $m$ is the total number of edges in the network.
- $\delta(c_i, c_j)$ is the Kronecker delta function, which is 1 if nodes $i$ and $j$ are in the same community ($c_i = c_j$), and 0 otherwise.
- $\frac{k_i k_j}{2m}$represents the expected number of edges between $i$ and $j$ in a random network with the same degree distribution as the original network.

## Interpretation

- **High Modularity:** Values close to 1 indicate strong community structure, meaning nodes within communities are densely connected, and nodes between communities are sparsely connected.
- **Low or Negative Modularity:** Values close to 0 or negative suggest that the community structure is no better than random, indicating weak or no meaningful community structure.

## Use in Community Detection

Modularity is used as an objective function in many community detection algorithms, such as the Louvain method. These algorithms aim to maximize the modularity score to identify the most meaningful division of the network into communities.

## Example

Consider a network divided into two communities. If most edges are within the same community and few edges connect different communities, the modularity will be high. Conversely, if edges are randomly distributed without a clear community structure, the modularity will be low or even negative.

## Summary
Modularity provides a single metric to evaluate and compare different community structures within networks. Its ability to highlight dense intra-community connections and sparse inter-community connections makes it a powerful tool for understanding and analyzing complex networks.