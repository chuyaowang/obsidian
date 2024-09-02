# Network Adjacency Matrix

A network adjacency matrix is a mathematical representation of a graph or network. It is a square matrix used to represent a finite graph, where the elements of the matrix indicate whether pairs of vertices (or nodes) are adjacent or not in the graph.

## Definition and Structure

- **Vertices/Nodes**: The entities in the network (e.g., people, computers, cities).
- **Edges**: The connections between the entities (e.g., friendships, communication links, roads).

The adjacency matrix $A$ for a graph with $n$ vertices is an $n \times n$ matrix where each element $A_{ij}$ is defined as:

- $A_{ij} = 1$ if there is an edge from vertex $i$ to vertex $j$.
- $A_{ij} = 0$ if there is no edge from vertex $i$ to vertex $j$.

### Types of Graphs and Their Adjacency Matrices

1. **Undirected Graphs**:
   - Symmetric adjacency matrix.
   - $A_{ij} = A_{ji}$.

2. **Directed Graphs (Digraphs)**:
   - Asymmetric adjacency matrix.
   - $A_{ij} \neq A_{ji}$ if there is a directed edge from $i$ to $j$ but not from $j$ to $i$.

3. **Weighted Graphs**:
   - Entries in the matrix represent the weight of the edge.
   - $A_{ij}$ could be any non-negative value indicating the weight of the edge from $i$ to $j$.

4. **Unweighted Graphs**:
   - Entries are either 0 or 1, indicating the absence or presence of an edge.

### Example

#### Undirected Unweighted Graph

Consider a simple undirected graph with 4 vertices (A, B, C, D):

- A is connected to B and C.
- B is connected to A and D.
- C is connected to A.
- D is connected to B.

The adjacency matrix $A$ is:

$$A = \begin{pmatrix}
0 & 1 & 1 & 0 \\
1 & 0 & 0 & 1 \\
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
\end{pmatrix}
$$

#### Directed Unweighted Graph

Consider a directed graph with 3 vertices (X, Y, Z):

- X has a directed edge to Y.
- Y has a directed edge to Z.
- Z has a directed edge to X.

The adjacency matrix $A$ is:

$$
A = \begin{pmatrix}
0 & 1 & 0 \\
0 & 0 & 1 \\
1 & 0 & 0 \\
\end{pmatrix}
$$

#### Weighted Graph

Consider a weighted graph with 3 vertices (P, Q, R):

- P is connected to Q with weight 2 and to R with weight 3.
- Q is connected to R with weight 4.
- R has no outgoing edges.

The adjacency matrix $A$ is:

$$
A = \begin{pmatrix}
0 & 2 & 3 \\
0 & 0 & 4 \\
0 & 0 & 0 \\
\end{pmatrix}
$$

### Applications

- **Social Networks**: Representing connections between people.
- **Computer Networks**: Representing connections between computers or routers.
- **Biological Networks**: Representing interactions between proteins, genes, or other biological entities.
- **Transportation Networks**: Representing routes between cities or locations.

### Advantages

- **Simple Representation**: Easy to understand and visualize.
- **Efficient Access**: Quick access to check if an edge exists between two vertices.

### Disadvantages

- **Memory Usage**: Requires $O(n^2)$ space, which can be inefficient for large, sparse graphs.
- **Scalability**: Not suitable for very large graphs due to space constraints.

In summary, an adjacency matrix is a fundamental tool in graph theory and network analysis, offering a straightforward way to represent and manipulate graphs mathematically.