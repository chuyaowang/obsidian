# Directed Graph

## Definition

A directed graph (or digraph) is a graph that has directed edges. This means that each edge has a direction associated with it, indicating which vertex the edge is coming from and which vertex it is going to. In contrast, an undirected graph has undirected edges, which means that the direction of the edge is not important.

A directed graph can be represented by a set of vertices (also called nodes) and a set of edges. The vertices are the points in the graph, and the edges are the lines that connect the vertices. Each edge is associated with a pair of vertices, indicating the source and destination of the edge.

## Examples

Directed graphs can be used to represent a variety of real-world relationships. For example, a directed graph can be used to represent the flow of traffic on a road network, the flow of information in a computer network, or the flow of control in a computer program.

## Matrix Representation

A directed graph can be represented as a matrix by using a 2D array, where each row represents a vertex and each column represents a vertex. The value at a given row and column indicates whether or not there is an edge between the two vertices. In the example of A->B->C, the matrix would look like this:

| A | B | C |
| --- | --- | --- |
| 0 | 1 | 0 |
| 0 | 0 | 1 |

The value at row 0, column 1 is 1, indicating that there is an edge from vertex A to vertex B. The value at row 1, column 2 is 1, indicating that there is an edge from vertex B to vertex C. The values at all other cells are 0, indicating that there are no edges between the other pairs of vertices. Note that this method will create a [sparse](Sparsity.md) matrix.

## [Transformer](Transformer.md)

Transformers can be used to predict a node in a directed graph. Transformers are a type of neural network that are well-suited for working with sequential data, such as the edges in a directed graph. Transformers can be used to learn the relationships between the nodes in a graph, and they can be used to predict the next node in a sequence.

Here are some of the ways that transformers can be used to predict a node in a directed graph:

-   **Node classification:** Transformers can be used to classify nodes in a graph. For example, transformers can be used to classify nodes as being spam or not spam, or as being a person or an organization.
-   **Link prediction:** Transformers can be used to predict links between nodes in a graph. For example, transformers can be used to predict which nodes are likely to be connected by an edge, or which nodes are likely to be in the same community.
-   **Node embedding:** Transformers can be used to embed nodes in a graph. Node embeddings are vector representations of nodes that capture the relationships between the nodes. Node embeddings can be used for a variety of tasks, such as node classification and link prediction.

Transformers are a powerful tool that can be used to work with directed graphs. They can be used to learn the relationships between the nodes in a graph, and they can be used to predict the next node in a sequence.