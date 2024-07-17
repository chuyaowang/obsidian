# struc2vec

#paper 
[Paper](https://arxiv.org/pdf/1704.03165v3.pdf)
[Blog post](https://www.ultipa.com/document/ultipa-graph-analytics-algorithms/struc2vec): definitely read this

## Overview

Struc2vec is a [Graph Embedding](Graph%20Embedding.md) method that preserves the structural similarity of nodes such that structurally similar nodes have similar vector embeddings. Being structurally similar means the nodes' have homologous connections with their neighboring nodes.

The motivation is that structural similarity implies functional similarity. They could have comparable roles or functions within network, acting in parallel or redundant processes, or occupying similar structural positions in the network’s architecture. This insight can guide further biological investigations and interventions.

Struc2vec ensures that even if two structurally similar nodes are far apart in the network, they will have similar embeddings. Whereas [Proximity Guided Gene Embedding](Proximity%20Guided%20Gene%20Embedding.md) methods, such as [Node2Vec](Graph%20Neural%20Network.md#Node2Vec), cannot achieve this since they generate embeddings for a node based on its neighbors within a certain number of hops (network depth).
 
The choice between Node2Vec and Struc2Vec depends on the nature of downstream tasks:

- Node2Vec suits tasks prioritizing node homophily, capturing **similarity in attributes and connections**.
- Struc2Vec excels when tasks demand a focus on **local topology similarity**, preserving the structural relationships among nodes.
- This dichotomy essentially defines two non-exclusive ways nodes can be similar: having similar functions or having similar roles in the network.

## Measure Structural Similarity

The first step of struc2vec is computing the structural similarity between every pair of nodes in the graph.

The intuition is that if two nodes have similar degrees, they are similar. If their neighbors also have similar degrees, they are even more similar.

Consider an undirected, unweighted graph $G = (V, E)$, its diameter is denoted as $k^*$. Let $R_k(u)$ denote the set of nodes located at an exact distance (hop count) of $k ∈ [0, k*]$ from node $u$ within $G$. Let $s(S)$ denote the _ordered degree sequence_ of a node set $S ⊂ V$.

$⊂$: means **a proper subset of**

Basically, for each $v \in V$, the [Node Degree](Node%20Degree.md)s of their neighbors is computed.  

The ordered degree sequence for each node represents their neighborhood connection structure. The **structural distance** between two nodes are then computed using [Dynamic Time Warping](Dynamic%20Time%20Warping.md) with a distance metric. 

In the paper [Gene2role a role-based gene embedding method for comparative analysis of signed gene regulatory networks](Gene2role%20a%20role-based%20gene%20embedding%20method%20for%20comparative%20analysis%20of%20signed%20gene%20regulatory%20networks.md), the [Exponential Based Euclidean Distance](Exponential%20Based%20Euclidean%20Distance.md) was used to account for [Power Law](Power%20Law.md) distribution of the nodes' degrees.

Let $f_{k}(u,v)$ denote the **structural distance** between $u$ and $v$ when considering their $k$-hop neighborhoods (all nodes at distance less than or equal to $k$).

Note that $f_{k}(u,v)$ is non-decreasing in $k$ and is _defined_ only when both $u$ and $v$ have neighbors at distance $k$.

## Multi-layer Weighted Graph

The structural distances are encoded in a multi-layer weighted graph. Each layer of the graph is formed by a _weighted undirected complete graph_ with node set V.
- Weighted: each edge has a weight associated with it
- Undirectly: the edges are undirected
- Complete graph: every pair of vertices are connected

This means that in this new graph, the edges are defined by the structural similarity of the nodes and not the same as the edges in the original graph, which could be gene regulation relationships or social media interactions, etc.

The graph and weighted edges serve an important role in the next step, random walk. Edges with higher weights are more likely to be traversed.

There are k layers in total, and the weights in layer k is defined as $$w_{k}(u,v)=e^{-f_{k}(u,v)}$$
This weight is inversely proportional to their structural distance, meaning that edges between structurally similar nodes (lower distance) have higher weights.

Note that the weight is a function of $k$. As the layer gets higher, more and more nodes will be considered as neighbors. For example, in layer 0, only the degrees of the two nodes $u$ and $v$ will be used to calculate their 
structural distance. In layer 3, all the nodes within their 3 hop distance will be used to calculate their structural distance. This means that in higher layers, _the similarity criteria gets more stringent_.

Edges are only defined when $f_{k}(u,v)$ is defined. When $u$ or $v$ does not have neighbors at $k$, there is no edge between them.

There are also inter-layer edges. Each node is connected to its counterparts in the layers above and below. The weight of the inter-layer edges are defined as $$\begin{aligned}
w(u_k,u_{k+1})&=log(\Gamma_{k}(u)+e)\\
w(u_k,u_{k-1})&=1\\
\end{aligned}$$ $\Gamma_{k}(u)$ measures the number of edges incident to $u$ with a weight higher than the average weight of the layer. If the weight is indeed higher, then it means this node has many similar nodes in this layer, and it will have a higher weight for the edge connecting to a higher layer.

It is like a level up system. Only the nodes structurally similar enough to others will connect to its counterparts in higher levels with a high weight. This also means that in higher levels, the average weight increases, since the dissimilar nodes do not get high in the multi-layer graph.

Therefore, in higher layers, only truly structurally similar nodes are connected by a highly weighted edge.

## Random Walk

A random walk with a fixed number of steps is started at the bottom layer. Its probabilities for moving to a different node, to a higher layer, and a lower layer are determined by the weights of inter- and intra-layer edges. It is more likely to move between similar nodes.

The process is repeated many times to generate many sequences of movements. These serve as the _context_
of the given node.

The sequences of nodes visited during random walks are used to train a skip-gram model, similar to the one used in word2vec. This model learns embeddings by predicting the context (surrounding nodes) of each node in the walks. Nodes that frequently appear in similar contexts across the random walks will have similar embeddings.

By considering the context in which nodes appear, the embeddings capture not just direct connections but also indirect relationships and structural roles. This is particularly important for identifying nodes that play _similar roles in different parts of the graph_.

