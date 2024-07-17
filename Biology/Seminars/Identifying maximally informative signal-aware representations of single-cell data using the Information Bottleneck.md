# BioIB

[BioIB paper](https://www.biorxiv.org/content/10.1101/2024.05.22.595292v1)
[Local Copy](bioIB.pdf)
[github](https://github.com/nitzanlab/bioIB)
#paper 

difference between doing ANOVA or PLS-DA?
identify cell subpopulations, metagene grouping, hierarchy
outperforms baseline clustering method

## Abstract

Utilizes the information bottleneck algorithm on [scRNA-seq](scRNA-seq.md) data.

The goal is to extract an optimal compressed representation of scRNA-seq data with respect to a desired **biological signal**, such as cell type or disease state.

BioIB generates a hierarchy of weighted gene clusters, termed **metagenes** that maximizes the information regarding the signal of interest.

It can also be used to identify biological signal-associated **cell subpopulations** in dataset.

The **metagene hierarchy** represents interconnections between the corresponding biological processes and cellular populations.

### Information bottleneck

Finding a balance between model complexity and information retained. In deep learning, the number of hidden layers can be reduced to force the model to extract only the most important part of the data.

## Introduction

Cell can be defined with various labels, such as cell type, disease state, developmental stages, etc. However, revealing which genes contribute to cell identity is challenging due to the high dimensionality of the cell $\times$ gene matrix. 

When aiming to uncover factors related to a specific biological signal, it is a trade-off between reducing the complexity of the data vs. retain as much relevant information as possible.

The bioIB algorithm outputs a compressed representation of scRNA data with **metagenes**, which are clustered probabilistic mapping of genes. The probabilistic construction preserves gene-level biological _interpretability_, allowing characterization of each metagene.

Compared with dimensionality reduction techniques such as PCA, bioIB takes into account the biological signal. Compared with deep learning clustering methods, BioIB is more interpretable.

BioIB also outputs a hierarchy of metagenes, reflecting the inherent data structure relative to the signal of interest, elucidating their significance in distinguishing between biological labels, and illustrating their interrelations with both one another and the underlying cellular populations. 

## Results

$\in$ : means *a member of*
$\forall$: means *for all*
$R$ means real numbers

### bioIB elucidates signal-specific metagenes and their structure

Input to bioIB: a count matrix $X\in{R^{N\times{G}}}$, where N is the number of cells and G the number of genes; a vector of cell labels $S\in{R^{N\times1}}$. 

BioIB outputs a compressed representation $\hat{X}\in{R^{N\times{M}}}$ of $N$ cells and $M$ metagenes, which optimizes tradeoff between compression and information about the signal of interest, denoted by $Y\in{R^K}$. $Y$ is all possible cell states, like {disease, healthy}. $S$ must be a member of $Y$, or $\forall{i}$, $S_i\in{Y}$. Metagenes signify major patterns of gene expression variation underlying the labeled signal.

$\hat{X}$ is obtained by minimizing the **mutual information** with the original data $X$, representing complexity, and maximizing the mutual information with the label $Y$, representing accuracy. $$\hat{X} = argmin_\hat{X}(I(X,\hat{X})-\beta{I(\hat{X},Y)})$$
The parameter $\beta$ determines the the level of compression. When it is $\infty$, it means only maximize accuracy, or no compression, $X=\hat{X}$. When it is 0, it means only minimize complexity, or cluster all genes into 1 cluster. Hence, $\beta$ determines the number of clusters. The hierarchy of metagenes is obtained by gradually decreasing $\beta$ in a reverse-annealing process.

The probabilistic output mapping $p(y|\hat{x})$ reflects the amount of information each metagene holds regarding the different labels, whereas the hierarchical structure reveals the interdependence between the metagenes, and the underlying cellular populations they correspond to. 

Plotting $p(y|\hat{x})$ against different $\beta$ reveals the branching of metagenes. Plotting $p(x|\hat{x})$ reveals which genes belong to which metagene. See figure 1E and 1F.

bioIB can also capture the relationships between related cell types, defined as the distinct labels of interest ($Y$). In a similar way to figure 1E, it reveals how two cell types can be connected.

### bioIB extracts distinct molecular signatures in macrophages for developmental stage and organ residence across development

Heterogeneity can be attributed to multiple factors, like organ of origin and developmental stage. Using bioIB, different compression of data can be achieved by selecting different signals of interest.

Chose to look at macrophages. 

Looking at the hierarchy, found a metagene specific to late gestational stage. GO analysis found they are enriched for immune processes. 

Setting $Y$ to organ of origin, metagenes that reflect organ signatures are found.

### bioIB metagenes identify Alzheimer's Disease associated astrocytes

Not all cells from a disease dataset are disease associated. bioIB helps finding those disease associated cells.

Given disease and wild type astrocytes, bioIB found 6 metagenes. Out of metagenes 0, 1, and 2 associated with AD cells, metagenes 1 and 2 are exclusively represented by AD-associated genes. Their associated cells are therefore directly disease associated cells.

In the original analysis, the cells were clustered into 6 clusters. Metagenes 1 and 2 are highly expressed in the original AD clusters.

Hence, bioIB helps identifying disease associated cells without pre-clustering of cells.

### bioIB metagene hierarchy reflects the developmental connections between hematopoietic cell types

bioIB can be used to study the developmental hierarchy of cells.

Looked at 6 hematopoietic cell types that have developmental relationship.

Found 11 metagenes. Metagene by cell type plot reveals some are uniquely expressed in 1 cell type. Some are expressed in multiple cell types. The cell type associated with every metagene is the one that maximizes $p(y|\hat{x})$.

Developmentally linked cell types have metagenes that are linked in the metagene hierarchy. The development hierarchy of cell types is inferred from graph diffusion distances between the cell types in a k nearest neighbor graph. 

## Discussion

- The algorithm is sensitive to the clusters' size. Clusters with small number of genes or cells are characterized by small number of metagenes. This can be a problem when studying rare populations and can be solved by sampling genes to create an uniform cluster distribution.
- The algorithm is limited to data size as an exact solution for the information bottleneck algorithm needs to be computed. This can be solved by analyzing the highly informative genes.
	- The authors used scanpy's `sc.pp.highly_variable_genes()` to select 500 highly variable genes.
- Future development will focus on extracting metagenes with respect to multiple signals of interest or other types of data.