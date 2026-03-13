# Transforms

The transform library on the [page](https://pytorch-geometric.readthedocs.io/en/latest/modules/transforms.html) you’re viewing is large, but it naturally clusters into **functional groups** that map well to common GNN tasks such as node classification, link prediction, graph classification, geometric learning, and positional encoding. The summary below organizes the transforms by *what problem they help solve*, with short explanations and examples.

---

## 🧱 General-purpose transforms (data preparation, normalization, splitting)

These transforms modify `Data` objects in ways that are useful across *all* GNN tasks.

### Useful for: node classification, link prediction, graph classification

- **ToDevice** — moves all tensors to CPU/GPU.  
- **ToSparseTensor** — converts `edge_index` into a `SparseTensor` adjacency (needed for some GNN layers).  
- **NormalizeFeatures** — row-normalizes node features.  
- **SVDFeatureReduction** — reduces feature dimensionality via SVD.  
- **Constant** — appends a constant feature to each node.  
- **Pad** — pads tensors to uniform shapes (useful for batching).  
- **IndexToMask / MaskToIndex** — converts between index lists and boolean masks.

### Useful for dataset splitting

- **RandomNodeSplit** — creates `train_mask`, `val_mask`, `test_mask` for node classification.  
- **RandomLinkSplit** — creates train/val/test edge splits for link prediction.  
- **NodePropertySplit** — creates splits with distributional shift (robustness testing).  
- **RemoveTrainingClasses** — removes some classes from training (zero-shot scenarios).

---

## 🔗 Graph-structure transforms (edge manipulation, topology changes)

These transforms modify the graph connectivity and are especially relevant for **node classification**, **link prediction**, and **graph classification**.

### Basic structural transforms

- **ToUndirected** — adds reverse edges to make the graph undirected.  
- **AddSelfLoops / AddRemainingSelfLoops** — adds self-loops (needed for GCN).  
- **RemoveSelfLoops** — removes self-loops.  
- **RemoveDuplicatedEdges** — removes duplicate edges.  
- **RemoveIsolatedNodes** — removes nodes with no edges.  
- **LargestConnectedComponents** — extracts the largest connected subgraph.

### Feature engineering from structure

- **OneHotDegree** — adds degree as one-hot features.  
- **TargetIndegree** — stores normalized indegree of target nodes.  
- **LocalDegreeProfile** — adds degree statistics (LDP baseline).

### Higher-order structure

- **TwoHop** — adds 2-hop edges.  
- **LineGraph** — converts graph to its line graph (edges become nodes).  
- **AddMetaPaths / AddRandomMetaPaths** — adds meta-path edges for heterogeneous graphs.

### Graph diffusion and normalization

- **GDC** — applies Graph Diffusion Convolution (diffusion-based reweighting).  
- **GCNNorm** — applies GCN normalization to adjacency.  
- **SIGN** — precomputes multi-hop features for scalable GNNs.

### Subgraph extraction

- **RootedEgoNets** — extracts k-hop ego-nets.  
- **RootedRWSubgraph** — extracts random-walk-based subgraphs.

---

## 📍 Positional and structural encodings (for expressive GNNs)

These transforms add positional information to nodes, improving performance in **node classification**, **graph classification**, and **link prediction**.

- **AddLaplacianEigenvectorPE** — Laplacian eigenvector positional encodings.  
- **AddRandomWalkPE** — random-walk positional encodings.  
- **AddGPSE** — Graph Positional and Structural Encoder features.  
- **FeaturePropagation** — propagates features to fill missing values.  
- **VirtualNode** — adds a virtual node connected to all nodes (improves message passing).

---

## 🌐 Geometric transforms (point clouds, meshes, spatial graphs)

These transforms are used in **vision**, **point cloud processing**, and **geometric deep learning**.

### Graph construction from geometry

- **KNNGraph** — builds edges using k-nearest neighbors in `data.pos`.  
- **RadiusGraph** — connects nodes within a radius.  
- **ToDense** — converts sparse adjacency to dense.

### Coordinate-based edge features

- **Distance** — stores Euclidean distances as edge attributes.  
- **Cartesian / LocalCartesian** — stores relative Cartesian coordinates.  
- **Polar / Spherical** — stores polar or spherical coordinates.  
- **PointPairFeatures** — rotation-invariant geometric features.

### Point cloud augmentation

- **Center** — centers point cloud.  
- **NormalizeRotation** — rotates points using PCA.  
- **NormalizeScale** — normalizes to (−1, 1).  
- **RandomJitter / RandomFlip / RandomScale / RandomRotate / RandomShear** — geometric augmentations.  
- **LinearTransformation** — applies a fixed transformation matrix.

### Mesh transforms

- **FaceToEdge** — converts mesh faces to edges.  
- **SamplePoints / FixedPoints** — samples points from meshes or point clouds.  
- **GenerateMeshNormals** — computes normals.  
- **Delaunay** — computes Delaunay triangulation.

### Image-to-graph transforms

- **ToSLIC** — converts an image into a superpixel graph.  
- **GridSampling** — voxelizes point clouds.

---

## 🧭 How to choose transforms by task

### Node classification

- NormalizeFeatures  
- ToUndirected  
- AddSelfLoops  
- GCNNorm  
- RandomNodeSplit  
- AddLaplacianEigenvectorPE / AddRandomWalkPE  
- LocalDegreeProfile  

### Link prediction

- RandomLinkSplit  
- ToUndirected  
- RemoveSelfLoops  
- TwoHop  
- GDC  
- AddMetaPaths (heterogeneous graphs)

### Graph classification

- KNNGraph / RadiusGraph (if building graphs from points)  
- LocalDegreeProfile  
- VirtualNode  
- NormalizeFeatures  
- LargestConnectedComponents  

### Geometric learning (point clouds, meshes)

- KNNGraph / RadiusGraph  
- Distance / Cartesian / Polar  
- NormalizeScale / Center  
- RandomJitter / RandomRotate  
- FaceToEdge / SamplePoints  

### Heterogeneous graph tasks

- AddMetaPaths  
- AddRandomMetaPaths  
- ToSparseTensor  

---

## 🧪 Minimal examples of using transforms

### Apply transforms implicitly through a dataset

```python
import torch_geometric.transforms as T
from torch_geometric.datasets import TUDataset

transform = T.Compose([
    T.ToUndirected(),
    T.AddSelfLoops(),
    T.NormalizeFeatures(),
])

dataset = TUDataset(root='data/MUTAG', name='MUTAG', transform=transform)
data = dataset[0]  # transformed automatically
```

### Apply transforms explicitly

```python
data = dataset[0]
data = T.ToUndirected()(data)
data = T.AddSelfLoops()(data)
```

### Build a graph from point clouds

```python
dataset = ShapeNet(
    root='data/ShapeNet',
    pre_transform=T.KNNGraph(k=6),
    transform=T.NormalizeScale()
)
```
