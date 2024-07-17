# Network Topology

chatgpt answer. double check the formulae before use.

## Degree Centrality

**Definition:** Degree centrality is a measure of the number of direct connections a node has in a network. It reflects the immediate risk of a node for catching whatever is flowing through the network (such as information or disease).

**Formula:** For an undirected graph, the degree centrality $C_D(v)$ of a node $v$ is given by:
$C_D(v) = \text{deg}(v)$
where $\text{deg}(v)$ is the degree of node $v$, i.e., the number of edges connected to $v$.

## Betweenness Centrality

**Definition:** Betweenness centrality measures the extent to which a node lies on the shortest paths between other nodes. It indicates the amount of influence a node has over the flow of information between other nodes in the network.

**Formula:** The betweenness centrality $C_B(v)$ of a node $v$ is given by:
 $C_B(v) = \sum_{s \neq v \neq t} \frac{\sigma_{st}(v)}{\sigma_{st}}$ 
where $\sigma_{st}$ is the total number of shortest paths from node s to node t, and $\sigma_{st}(v)$ is the number of those paths that pass through v.

## Eigenvector Centrality

**Definition:** Eigenvector centrality assigns relative scores to all nodes in the network based on the principle that connections to high-scoring nodes contribute more to the score of the node in question. It is a measure of the influence of a node in a network.

**Formula:** The eigenvector centrality $x_i$ of a node i is defined by the eigenvector equation:
$\mathbf{x} = \lambda \mathbf{A} \mathbf{x}$ 
where $\mathbf{A}$ is the adjacency matrix of the network, $\lambda$ is the largest eigenvalue of $\mathbf{A}$, and $\mathbf{x}$ is the eigenvector corresponding to $\lambda$. Each element $x_i$ in $\mathbf{x}$ is the eigenvector centrality of node $i$.

## Degree Assortativity

**Definition:** Degree assortativity measures the tendency of nodes to connect to other nodes with similar degree. It is a correlation coefficient between the degrees of nodes at either end of a link.

**Formula:** The assortativity coefficient r for degree is given by:
 $r = \frac{\sum_{jk} jk (e_{jk} - q_j q_k)}{\sigma_q^2}$
where $e_{jk}$ is the joint probability distribution of the degrees of the two nodes at either end of a randomly chosen edge, $q_k$ is the distribution of the remaining degrees (the degree of a node minus one), and $\sigma_q$ is the standard deviation of the distribution $q_k$.

## Clustering Coefficient

**Definition:** The clustering coefficient measures the degree to which nodes in a graph tend to cluster together. It indicates how likely it is that the neighbors of a node are also connected to each other.

**Formula:** For a node v, the local clustering coefficient $C(v)$ is given by:
 $C(v) = \frac{2E(v)}{\text{deg}(v)(\text{deg}(v) - 1)}$
where $E(v)$ is the number of edges between the neighbors of $v$, and $\text{deg}(v)$ is the degree of node v. The global clustering coefficient is the average of the local clustering coefficients of all nodes in the network.

These metrics are fundamental in network analysis and help in understanding the structure and behavior of complex networks.