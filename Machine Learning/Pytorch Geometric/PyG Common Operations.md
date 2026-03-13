# Common Operations

A practical way to understand PyTorch Geometric is to look at how it handles **graph data**, **datasets**, **mini‑batches**, and **transforms**. The [documentation page](https://pytorch-geometric.readthedocs.io/en/latest/get_started/introduction.html) lays out these concepts clearly, and the guide below distills them into a structured reference with code snippets and explanations grounded in that page’s content.

---

## 🧱 Graph data objects (`torch_geometric.data.Data`)

A `Data` object is the fundamental container for a single graph. It stores node features, edges, labels, and any additional attributes you want.

### What a `Data` object can contain

- **`x`** — node feature matrix `[num_nodes, num_node_features]`
- **`edge_index`** — graph connectivity in COO format `[2, num_edges]`, `torch.long`
- **`edge_attr`** — edge features `[num_edges, num_edge_features]`
- **`y`** — labels (node‑level or graph‑level)
- **`pos`** — node positions (for geometric data)
- **Custom attributes** — e.g., `face` for meshes

These fields are optional; PyG does not enforce a fixed schema. The documentation emphasizes this flexibility.

### Creating a simple graph

The method below uses two lists containing the source and target of all edges, not a list of index tuples.

```python
import torch
from torch_geometric.data import Data

edge_index = torch.tensor([[0, 1, 1, 2],
                           [1, 0, 2, 1]], dtype=torch.long)

x = torch.tensor([[-1.0], [0.0], [1.0]], dtype=torch.float)

data = Data(x=x, edge_index=edge_index)
print(data)
```

This creates a 3‑node undirected graph with 4 directed edges (because undirected edges are stored twice).

Alternatively, the edges can be defined as pairs of index tuples. An additional transform is required to use it as the edge index.

``` python
import torch
from torch_geometric.data import Data

edge_index = torch.tensor([[0, 1],
                           [1, 0],
                           [1, 2],
                           [2, 1]], dtype=torch.long)
x = torch.tensor([[-1], [0], [1]], dtype=torch.float)

data = Data(x=x, edge_index=edge_index.t().contiguous())
>>> Data(edge_index=[2, 4], x=[3, 1])
```

### Useful utilities

```python
data.num_nodes
data.num_edges
data.num_node_features
data.is_undirected()
data.has_self_loops()
data.validate(raise_on_error=True)
```

These help you inspect and verify your graph structure.

---

## 📚 Benchmark datasets

PyG includes many standard graph datasets. Initializing a dataset automatically downloads and processes it into `Data` objects.

### Example: ENZYMES (graph classification)

```python
from torch_geometric.datasets import TUDataset

dataset = TUDataset(root='/tmp/ENZYMES', name='ENZYMES')
print(len(dataset))          # 600 graphs
print(dataset.num_classes)   # 6
print(dataset.num_node_features)
```

Each item is a separate graph:

```python
data = dataset[0]
print(data)  # Data(edge_index=[2, 168], x=[37, 3], y=[1])
```

### Example: Cora (node classification)

Cora contains **one** large citation graph with masks for train/val/test splits.

```python
from torch_geometric.datasets import Planetoid

dataset = Planetoid(root='/tmp/Cora', name='Cora')
data = dataset[0]
print(data.train_mask.sum())  # 140 training nodes
```

These masks are described directly in the documentation   [pytorch-geometric.readthedocs.io](https://pytorch-geometric.readthedocs.io/en/latest/get_started/introduction.html).

### Splitting datasets

```python
train_dataset = dataset[:540]
test_dataset = dataset[540:]
```

### Shuffling datasets

```python
dataset = dataset.shuffle()
```

---

## 🧩 Mini‑batches for multiple graphs

When training on many graphs (e.g., ENZYMES), PyG batches them by:

- stacking node features,
- stacking labels,
- building a **block‑diagonal adjacency matrix** from all `edge_index` tensors.

This allows graphs of different sizes to be processed together. The documentation explains this batching mechanism explicitly.

### Using a DataLoader

```python
from torch_geometric.loader import DataLoader

loader = DataLoader(dataset, batch_size=32, shuffle=True)

for batch in loader:
    print(batch)
```

A batch is a `DataBatch` object:

- `batch.x` — concatenated node features
- `batch.edge_index` — block‑diagonal adjacency
- `batch.batch` — vector mapping each node to its graph ID

### Example: aggregating per‑graph features

```python
from torch_geometric.utils import scatter
from torch_geometric.datasets import TUDataset
from torch_geometric.loader import DataLoader

dataset = TUDataset(root='/tmp/ENZYMES', name='ENZYMES', use_node_attr=True)
loader = DataLoader(dataset, batch_size=32, shuffle=True)

for data in loader:
    data
    >>> DataBatch(batch=[1082], edge_index=[2, 4066], x=[1082, 21], y=[32])

    data.num_graphs
    >>> 32

    x = scatter(data.x, data.batch, dim=0, reduce='mean')
    x.size()
    >>> torch.Size([32, 21])
```

---

## 🔧 Data transforms

Transforms modify graphs either:

- **before saving** (`pre_transform`)  
- **each time they are loaded** (`transform`)

Transforms operate on `Data` objects and return new ones.

### Example: converting point clouds to graphs

```python
import torch_geometric.transforms as T
from torch_geometric.datasets import ShapeNet

dataset = ShapeNet(
    root='/tmp/ShapeNet',
    categories=['Airplane'],
    pre_transform=T.KNNGraph(k=6)
)
```

This adds edges based on k‑nearest neighbors. When the saved data is loaded, the transform is already applied.

### Example: augmenting data on the fly

```python
dataset = ShapeNet(
    root='/tmp/ShapeNet',
    categories=['Airplane'],
    pre_transform=T.KNNGraph(k=6),
    transform=T.RandomJitter(0.01)
)
```

Transforms are chained using `T.Compose`.

---

## 🧠 Putting it all together: common PyG workflow

### 1. Load or create graphs

```python
data = Data(x=x, edge_index=edge_index)
```

### 2. Load a dataset

```python
dataset = TUDataset(root='/tmp/ENZYMES', name='ENZYMES')
```

### 3. Apply transforms

```python
dataset = TUDataset(root, name, pre_transform=T.KNNGraph(6))
```

### 4. Create mini‑batches

```python
loader = DataLoader(dataset, batch_size=32, shuffle=True)
```

### 5. Train a GNN

```python
for batch in loader:
    out = model(batch)
    loss = criterion(out, batch.y)
```
