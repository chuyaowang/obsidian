# A systematic review of biologically-informed deep learning models for cancer: fundamental trends for encoding and interpreting oncology data

[paper link](https://link.springer.com/article/10.1186/s12859-023-05262-8)
#paper
[Beyond the black box with biologically informed neural networks](Biology/Seminars/Beyond%20the%20black%20box%20with%20biologically%20informed%20neural%20networks.md)

## Abstract

- Explainable deep learning used to integrate multi-omics data and study cancer
- How existing models use prior knowledge, biological plausibility, and interpretability
- Integrating prior biological relational and network knowledge such as pathways or PPI networks
- Outlook: convergence between encoding prior knowledge and improved interpretability

---

## Background

- DL for oncology analysis -> precision and personalized medicine
- Integrating multi-omics better than single omics
- Addresses existing paradigmatic analytical gaps: small sample size and large number of features
- the dialogue and convergence between biologically-informed models, explainable AI (XAI) and biological interpretability
- motifs within emerging architectures
	- the domain knowledge, used for designing the model
	- data representation
	- common architectures: from biological networks to graphs to embedding models
- bio-centric interpretability
	- augments XAI taxonomies
	- a fundamental property and desideratum of biologically informed DL

## Result

### Bio-centric model interpretability

- Mapping of model components to biological mechanisms, delivering an interpretation for the intended user which relies on more biological rather than on DL or math knowledge
- The authors introduce the concept of **bio-centric interpretability**, which integrates:
     - **Architecture-Centric Interpretability**: Embedding biological mechanisms into model design.
     - **Output-Centric Interpretability**: Linking model predictions to biological processes.
     - **Post-Hoc Biological Plausibility**: Validating model outputs against known biological knowledge.
- They argue all three need to be analyzed to evaluate DL models for their bio-centric interpretability
- The 3 aspects are analyzed via the analysis of 4 bio-centric interpretability components:
	- **integration of different data modalities**: different omics data
	- **the schema level representation of the model**: understanding the data flow and transformation (from a sample x feature matrix to graphs, eigenvectors, networks, etc.)
	- **the integration of domain knowledge (DK)**: make use of databases of biological relations
	- **post-hoc explainability methods**: track back the flow of information through the network to understand the latent features derived by the network

### Integration of domain knowledge

 - The review categorizes methods for incorporating domain knowledge into DL models:
     - **Pre-Processing**: Enriching input data with biological annotations.
     - **Architecture Design**: Structuring models based on biological relationships (e.g., sparse connections reflecting pathways).
     - **Post-Hoc Analysis**: Validating outputs using curated biological databases.

![](Media/Pasted%20image%2020250319153346.png)

- DK (databases and expert knowledge) can be used to preprocess data into different forms suitable for different NN architectures
- DK can be used to inform connections to create a sparsely connected NN. ex. connects a gene to its transcription factor

---

## Discussion

### Prevalence of graph representations

[7. VU DL Learning from Graphs](Machine%20Learning/VU%20Deep%20Learning/7.%20VU%20DL%20Learning%20from%20Graphs.md)

- Increasing use of graph-based representations (e.g., [Graph Neural Network](Machine%20Learning/Concepts/Graph%20Neural%20Network.md)) to model biological interactions.
- GNNs can encode biological knowledge into neural representations
- Mapping topological relations into a high-dimensional embedding space
- Increase of GCN/GNN application using PPI networks as DK
	- assumption: interacting genes tend to produce similar phenotypes
- GNN and GCN are useful for combining heterogeneous omic data types with graph data representations into a predictive model and abstract features from both omic data and graph representations
- GNN/GCN uses the PPI network in the pre-processing stage to convert tabular data to graph and fed into the model.

### Prevalence of sparse connections

- Sparse connections between the nodes

---

## Authors' Conclusions

- Biologically-informed DL models represent a paradigm shift in cancer research, enabling both mechanistic and statistical inference.
- The concept of bio-centric interpretability provides a framework for developing models that are not only accurate but also biologically meaningful and actionable.

---

## Future Directions

1. **Standardizing Interpretability**:
   - Developing formal definitions and metrics for biological interpretability in DL models.
2. **Expanding Domain Knowledge Integration**:
   - Leveraging more comprehensive and diverse biological databases to enhance model design and validation.
3. **Clinical Translation**:
   - Bridging the gap between research and clinical practice by ensuring models are robust, interpretable, and validated in real-world settings.