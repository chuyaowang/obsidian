# Hungarian Algorithm

[Wikipedia](https://en.wikipedia.org/wiki/Hungarian_algorithm)

## Optimal assignment problem

- The Hungarian algorithm solves the optimal assignment problem
	- How to assign $n$ tasks to $n$ people to minimize the cost?

### Matrix representation

- The problem can be represented as a cost matrix where the rows are tasks and columns are people and their costs for each task

| Task<br><br>Worker | Clean  <br>bathroom | Sweep  <br>floors | Wash  <br>windows |
| ------------------ | ------------------- | ----------------- | ----------------- |
| Alice              | **$8**              | $4                | $7                |
| Bob                | $5                  | $2                | **$3**            |
| Carol              | $9                  | **$4**            | $8                |

### Graph representation

- It can also be represented as a bipartite graph where one set of nodes are the tasks and the other are people, and they are connected by edges that represent costs

### The Hungarian algorithm

- The Hungarian algorithm can find the optimal assignment in the matrix or the graph representation
	- Matrix: can be expressed as permuting the rows of a cost matrix _C_  to minimize the [trace](https://en.wikipedia.org/wiki/Trace_\(linear_algebra\) "Trace (linear algebra)") of a matrix
	- Graph: We have a [complete bipartite graph](https://en.wikipedia.org/wiki/Complete_bipartite_graph "Complete bipartite graph") $G=(S,T;E)$ with n worker vertices ($S$) and n job vertices ($T$), and the edges ($E$) each have a cost $c(i,j)$. We want to find a [perfect matching](https://en.wikipedia.org/wiki/Perfect_matching "Perfect matching") with a minimum total cost.
- Minimum time complexity is $O(n^{3})$

## Graph representation

### 1. Primal and Dual Problems

#### General LP meaning

- **Primal problem**: The original optimization problem you want to solve.
- **Dual problem**: A related problem derived from the primal’s constraints and objective.
    - Any feasible dual solution gives a bound on the primal’s optimal value (**weak duality**).
    - Under certain conditions, the optimal values of the primal and dual are equal (**strong duality**).

---

#### In the Hungarian algorithm

We model the **assignment problem** as a **minimum-cost perfect matching** in a bipartite graph:

- **Sets**:  
    $S$ = workers, $T$ = jobs  
    $c(i,j)$ = cost of assigning worker $i \in S$ to job $j \in T$
    
- **Primal LP** (minimum-cost perfect matching):
    

$$\begin{aligned} \text{Minimize:} \quad & \sum_{i \in S} \sum_{j \in T} c(i,j) , x_{ij} \ \\\text{Subject to:} \quad & \sum_{j \in T} x_{ij} = 1 \quad \forall i \in S \ \\& \sum_{i \in S} x_{ij} = 1 \quad \forall j \in T \ \\& x_{ij} \ge 0 \end{aligned}$$

Here $x_{ij} = 1$ if $i$ is matched to $j$, else $0$.

- **Dual LP**:

$$\begin{aligned} \text{Maximize:} \quad & \sum_{v \in S \cup T} y(v) \ \\\text{Subject to:} \quad & y(i) + y(j) \le c(i,j) \quad \forall i \in S, j \in T \end{aligned}$$

---

### 2. How this leads to the “Potential”

In the bipartite graph formulation, the **dual variables** $y(v)$ are called **potentials**.

- **Definition**:  
    A function $y : S \cup T \to \mathbb{R}$ is a **potential** if: $$y(i) + y(j) \le c(i,j) \quad \forall i \in S, j \in T$$
- **Value of a potential**: $$\text{val}(y) = \sum_{v \in S \cup T} y(v)$$
- **Weak duality**: For any perfect matching $M$ and any potential $y$: $$\text{val}(y) \le \text{cost}(M)$$ because each edge cost is at least the sum of its endpoint potentials, and a perfect matching covers every vertex exactly once.

---

### 3. How the Hungarian Algorithm Uses the Potential

The Hungarian method maintains **two objects**:

1. A **matching** $M$ in the bipartite graph.
2. A **potential** $y$ satisfying the dual feasibility condition.

**Key invariants**:

- All edges in ( M ) are **tight**: $$y(i) + y(j) = c(i,j)$$
- $M$ is feasible (no vertex matched more than once).
- $y$ is feasible (dual constraints hold).

**Algorithm flow**:

1. **Initialization**: Start with $y(v) = 0$ for all vertices, $M = \emptyset$ (M is empty, no matching).
2. **Tight edges**: Work only with edges where $y(i) + y(j) = c(i,j)$ — these form the **equality subgraph**.
3. **Augmenting paths**:
    - If there’s an alternating path from a free vertex in $S$ to a free vertex in $T$ using only tight edges, flip matched/unmatched edges along it to increase $|M|$. (See [Explanation of alternating path](https://yasenh.github.io/post/hungarian-algorithm-1/) for meaning)
4. **Adjust potentials**:
    - If no augmenting path exists, adjust $y$ by the smallest amount $\Delta$ that creates at least one new tight edge, preserving feasibility. (See [Medium post](https://medium.com/data-science/optimum-assignment-and-the-hungarian-algorithm-8b1027628028) for example)
5. **Repeat** until $M$ is a perfect matching.
6. **Optimality**: When $\text{val}(y) = \text{cost}(M)$, strong duality holds — both $M$ and $y$ are optimal.

#### Finding an augment path

In the **graph-based description** of the Hungarian algorithm,  
$\overrightarrow{G_y}$ is the **oriented equality subgraph** for the current potential $y$:

- **Equality subgraph $G_y$**: contains only the **tight edges** — edges $(i,j)$ where  
    $y(i) + y(j) = c(i,j)$.
- **Orientation**: edges in the current matching $M$ are directed **from $T$ to $S$**,  
    all other tight edges are directed **from $S$ to $T$**.

---

##### $R_S$

- $R_S$ is the set of **free (unmatched) vertices in $S$** — vertices in $S$ that have no incoming matched edge.

---

##### $Z$ definition

> “Let $Z$ be the set of vertices reachable in $\overrightarrow{G_y}$ from $R_S$ by a directed path.”

This means:

- Start from every vertex in $R_S$ (free vertices on the $S$ side).
- Follow the **directions** of edges in $\overrightarrow{G_y}$.
- Collect **all vertices** you can reach by some sequence of directed edges.
- The union of all such reachable vertices is $Z$.

---

##### Why this matters in the algorithm

- $Z$ is essentially the **search tree** (or alternating tree) grown from free vertices in $S$ using only tight edges, respecting the orientation.
- If $Z$ contains a free vertex in $T$, you’ve found an **augmenting path** — you can flip matched/unmatched edges along it to increase the matching size.
- If $Z$ contains **no** free vertex in $T$, the algorithm uses $Z$ to decide how to **adjust the potentials** $y$ to create new tight edges and enlarge $Z$ in the next iteration.

---

💡 **Intuition**:  
Think of $Z$ as “all vertices you can reach from the free (S)-side vertices by walking along the current tight-edge structure, following the alternating matched/unmatched pattern encoded in the edge directions.”

---

### Algorithm Intuition:

- The **primal** (matching) tries to minimize cost.
- The **dual** (potential) tries to maximize total vertex “prices” without exceeding edge costs.
- The Hungarian algorithm moves both in lockstep until they meet — at that point, you have the cheapest possible perfect matching.

## Matrix representation

We start with an $n \times n$ **cost matrix** $C$, where $C_{ij}$ is the cost of assigning worker $i$ to job $j$.

### Step 1 – Row reduction

- For each row, subtract the smallest entry in that row from **every** element in the row.
- This ensures each row has at least one zero.
- Interpretation: subtracting a constant from a row is like **increasing the potential** of that worker in the graph view.

---

### Step 2 – Column reduction

- For each column, subtract the smallest entry in that column from **every** element in the column.
- Now each column has at least one zero.
- Interpretation: subtracting a constant from a column is like **increasing the potential** of that job vertex.

---

### Step 3 – Cover zeros with minimum number of lines

- Try to assign tasks to workers using only zero entries (one per row/column).
- If you can assign all (n) workers, you’re done.
- If not, cover all zeros in the matrix with the **minimum number of horizontal and vertical lines**.

---

### Step 4 – Adjust uncovered elements

- Find the smallest uncovered value $\Delta$.
- Subtract $\Delta$ from all uncovered elements.
- Add $\Delta$ to all elements covered **twice** (by both a row and a column line).
- This creates new zeros without destroying existing assignments.
- Interpretation: this is exactly the **dual variable update** in the graph version — shifting potentials to create new tight edges.

---

### Step 5 – Repeat

- Go back to Step 3 with the updated matrix.
- Continue until you can assign all $n$ workers to $n$ jobs using only zeros.
- The positions of the assigned zeros give the **minimum-cost matching**.

---

## Equivalence of matrix representation to the graph interpretation

In the **graph formulation**:

- Vertices: $S$ = workers, $T$ = jobs.
- Edge weights: $c(i,j)$ = cost of assigning $i$ to $j$.
- **Potentials** $y(i)$ and $y(j)$ satisfy: $$y(i) + y(j) \le c(i,j)$$
- **Tight edges**: $y(i) + y(j) = c(i,j)$ — these correspond to **zeros** in the reduced cost matrix.

**Mapping between the two views**:

|Matrix operation|Graph interpretation|
|---|---|
|Subtract min from a row|Increase potential of worker vertex|
|Subtract min from a column|Increase potential of job vertex|
|Zero in matrix|Tight edge in equality subgraph|
|Covering zeros & adjusting uncovered values|Finding augmenting paths / adjusting potentials to create new tight edges|
|Final set of starred zeros|Perfect matching in equality subgraph|

**Why they’re equivalent**:

- The reduced cost matrix in the matrix method is exactly: $$C'_{ij} = c(i,j) - y(i) - y(j)$$
- Row/column subtractions are potential updates.
- Zeros in $C'$ are edges where reduced cost is zero — the equality subgraph.
- The process of covering zeros and adjusting uncovered values is the same as **growing the set (Z)** in the graph algorithm and updating potentials to expose new tight edges.
- When you can assign all workers to jobs using only zeros, you have a **perfect matching of tight edges**, which by strong duality is optimal.
