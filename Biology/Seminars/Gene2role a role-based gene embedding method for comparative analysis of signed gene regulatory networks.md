# Gene2role

#paper 
[Link](https://www.biorxiv.org/content/10.1101/2024.05.18.594807v1.full#ref-15)
[Github](https://github.com/liushu2019/g2r_work)
[Local copy](Gene2role.pdf)
University of Tokyo

A tool for comparative analysis of signed  [Gene Regulatory Network](Gene%20Regulatory%20Network.md).
similar to harmony for combining batches?

## Abstract

Comparing GRNs in various cell states reveals the underlying mechanisms governing cell behavior and functionality.

Current approaches are simple, often focus on simple topological information such as the [degree](Node%20Degree.md) of genes.

Developed Gene2role, a **gene embedding** approach that leverages multi-hop topological information from genes within signed GRNs.

## Introduction

Signed GRN: the edges are signed to represent _activation_ or _inhibition_.

### GRN Inference

- From regulatory relations from literature; limited to small networks
- Gene co-expression patterns across various conditions or tissues from [scRNA-seq](scRNA-seq.md) data
	- EEISP (2021 paper): GRNs from scRNA-seq data based on co-dependency and mutual exclusivity of gene expression
	- Hard to discern direct and indirect regulation using co-expression approach
- Single cell multi-omics
	- [CellOracle](Dissecting%20cell%20identity%20via%20network%20inference%20and%20in%20silico%20gene%20perturbation.md) (2023 paper): [scATAC-seq](scATAC-seq.md) and scRNA-seq data, leveraging [Transcription Factor](Transcription%20Factor.md) binding [motifs](1.%20MIT%20CompBio%20-%20Introduction.md#^6a1795) and co-expression information to infer GRNs
	- More detailed and comprehensive

### Downstream Analysis

Prevalent approach focuses on the topology of cell type specific GRNs to [identify key _TFs_ and _gene modules_](GRN%20Analysis.md). For example, important nodes tend to have many edges. Closely placed nodes can form a community, etc. These approaches focus on _one network_ and cannot compare GRNs in different cell states.

> [!summary] Gene Module
> A [Gene Module](Gene%20Module.md) is a group of genes regulated by the same set of TFs and have functional similarity.

When you want to compare GRNs, you want to look at how the topology changes, which is the essence of having a network.

Methods for comparing GRNs often focus on the direct [topological information](Network%20Topology%20Metrics.md) and overlook the deeper structural connections (their neighbors in the graph). This is not sufficient to understand the inherent complexities of GRNs.

[Graph Embedding](Graph%20Embedding.md) techniques can project genes into an embedding space. As these techniques retain the information about graph structure, they enable more precise quantification of gene distances. However, traditional methods relying on [proximity principles](Proximity%20Guided%20Gene%20Embedding.md), such as [Node2Vec](Graph%20Neural%20Network.md#Node2Vec), cannot project genes from different networks to a closely positioned space. Genes with similar functions could be positioned far away in the embedding space this way.

Two embedding methods: [struc2vec](struc2vec%20Learning%20Node%20Representations%20from%20Structural%20Identity.md) (Ribeiro et al. 2017) and SignedS2V (Liu et al. 2023) can efficiently integrate multiple graphs into one embedding space, allowing for nuanced comparisons of topological similarities across networks. This suits the comparative analysis of GRNs well.

### Paper

Gene2role employs struc2vec and SignedS2V. Experimented on multiple GRNs for Gene2role's ability to capture the topological information.

Gene2role embeddings were used to analyze genes that exhibit _structural variations_ across GRNs.
Connected to different nodes?

Also assessed the stability of _gene modules_ across different cell states.

## Methods

The framework consists of 3 parts:
1. Network construction
2. Embedding generation
	1. SignedS2V (signed struc2vec) for extracting the _topological features_ of genes in the signed GRN and calculating the _similarity_ between genes.
	2. struc2vec for gene embedding
3. Downstream analysis: at gene and module levels

### Network Preparation

- Simple simulated network; 31 genes
- Curated network from BEELINE: hematopoietic stem cell (HSC), mammalian cortical area development (mCAD), ventral spinal cord (VSC), gonadal sex determination (GSD); small networks, 5 to 19 genes
- from [scRNA-seq](scRNA-seq.md): human glioblastoma from 2 stages (0 and 12 hr), human bone marrow mononuclear cells (BMMC) and human peripheral blood mononuclear cells (PBMC)
	- for each cell type, count matrices were generated using the 2000 highly variable genes
	- cell type-specific GRNs generated using EEISP (also by their lab) and Spearman correlation
- [scRNA-seq](scRNA-seq.md) and [scATAC-seq](scATAC-seq.md) network from [Dissecting cell identity via network inference and in silico gene perturbation](Dissecting%20cell%20identity%20via%20network%20inference%20and%20in%20silico%20gene%20perturbation.md)
	- CellOracle integrates [scRNA-seq](scRNA-seq.md) and [scATAC-seq](scATAC-seq.md) data
	- Differentiating mouse myeloid progenitors across 24 cell states
	- Only connections exhibiting a p-value less than 0.01 were considered
	- Only main the top 2000 edges, chosen based on their highest absolute coefficient values
	- 521 to 642 genes

### Gene topological similarity in signed GRN

This part is done with signedS2V, where the struc2vec's [Measure Structural Similarity](struc2vec%20Learning%20Node%20Representations%20from%20Structural%20Identity.md#Measure%20Structural%20Similarity) method is adapted to measure structural distance for a signed GRN (the original works for unsigned GRNs). 

Since GRNs are typically [Scale-free Networks](Scale-free%20Network.md), some nodes can have significantly more connections than others. The distance is evaluated with [Exponential Based Euclidean Distance](Exponential%20Based%20Euclidean%20Distance.md) (EBED. First, the degrees are log transformed to make the values less extreme. After calculating the distance, an exponential function is applied to restore the original distance proportions.

### Embedding generation

The rest is pretty much identical to [struc2vec](struc2vec%20Learning%20Node%20Representations%20from%20Structural%20Identity.md):
- Generate ordered sequence of degrees in the $k_{th}$ hop neighborhood
- [Dynamic Time Warping](Dynamic%20Time%20Warping.md) to align two sequences and use EBED as the distance metric to calculate their distance in between
- Build a multilayer weighted graph in which weight of the edges are inversely proportional to structural distance
- Random walk and learn embedding with the skip-gram model

#### Hyperparameters

Needs to be adjusted obviously. See their supplementary note 2.

### Identifying differentially topological genes (DTGs)

DTGs are the same genes that are connected differently (or topologically variable) in the GRNs of different cell types.

This is determined by first finding a centroid for a gene in all the cell types then calculating the distance from each embedding to the centroid. Those genes with high average distances or high standard deviation are classified as DTGs.

Being DTGs implies genes undergo _role changes_ across cell states. Those with high average distance change across all cell states, while those with high standard deviation are stable in some states but variable in others.

Differentially expressed genes (DEGs) are identified with Seurat and compared with DTGs. DEGs are those genes with significant expression level change.

### Gene module stability analysis

[Gene Module](Gene%20Module.md)s are clusters of genes having similar functions or regulated by the same set of [Transcription Factor](Transcription%20Factor.md)s.

An _anchor cell type_ ($c_1$) was defined. Then gene modules in $c_1$'s GRNs were identified with the [Louvain Clustering Algorithm](Louvain%20Clustering%20Algorithm.md), a proximity based method. Gene modules containing fewer than 10 genes were excluded.

For each remaining module, average distance (over each gene in the module) between 2 cell types were calculated. This distance quantifies their topological deviation. 

Sometimes a gene exists in the anchor cell's gene module but not in the other cell type. This is quantified by NA%.

#### Biological functions of gene module

`compareCluster` function from the `clusterProfiler` package.

Used the `enrichGO` function, org.Hs.eg.db and org.Mm.eg.db as the GO database.

Benjamini-Hochberg method to adjust p-values, q-value cutoff set at 0.05 to determine significance.

Retained top 5 GO terms for each gene module retained.

### Baseline methods

[struc2vec](struc2vec%20Learning%20Node%20Representations%20from%20Structural%20Identity.md): role-based embedding but does not consider sign
BESIDE: consider sign information but proximity based

Did multiple comparisons. Showed gene2role is good at role-based embedding for signed GRNs.

### Evaluation metrics

Used to evaluate clusters of gene in GRN.

Metrics: see terms in [Network Topology Metrics](Network%20Topology%20Metrics.md). Evaluated separately for \+ and \- connections.

In their heatmap, the color scaling is based on the max and min of each metric, not the entire graph. Interesting technique.

Clusters visualized with UMAP and clustered with k means.

## Results

### Validating the method

#### Simple network

The simple networks were used to evaluate gene2role against struc2vec and BESIDE. It **shows** that gene2role can place genes with structural similarity closer together, while the other two failed to some extent.

#### scRNA network

Gene embeddings clustered with k means clustering. 

Computed [Network Topology Metrics](Network%20Topology%20Metrics.md) metrics for each cluster. **Shows** that each cluster has unique topology.

Compared clusters between two GRN inference methods, EEISP and Spearman correlation. **Shows** that the clusters captured similar sets of genes. Hence the embedding method works for different GRN inference methods.

#### Cell oracle network

Generated embeddings for the Ery_0 GRN (24 states in total) and clustered using k mean clustering.

Computed [topological metrics](Network%20Topology%20Metrics.md). **Showed** that each cluster contains genes with similar topology. Hence, gene2role works for complex networks as well.

### Analysis using the embeddings

#### Identification of DTGs between pairwise states

Merged two GRNs from 0 hr and 12 hr data and computed pairwise distance for each gene. Identified differentially topological genes (DTGs). Sometimes DTGs overlap with DEGs, meaning topology change accompanies expression level change. Sometimes only topology change or expression level change happens without affecting the other.

#### Identification of DTGs among multiple cell states

Similar as above except in multiple cell states.

#### Gene stability analysis

Evaluate gene stability, NA%, and GO analysis for multiple cell types.

## Discussion

Relative independence between expression level change and topology (role) change.

Remaining problems:
1. If a gene is not connected at all to the network in a GRN, it will not be embedded. Hence, even if it is connected to some other nodes in another network, a structural distance cannot be calculated.
2. The gene modules are defined in the anchor cell type using proximity based clustering. Gene module stability is then analyzed with respect to the gene modules in the anchor cell type. However, interesting changes may also take place in gene modules that are in the other cell types.

Also applicable to spatial transcriptomics data. Spatial GRNs can be inferred from expression information, spatial information, and histological information. Spatial GRNs can then be analyzed using this tool.

## Data 

The edgelists of curated networks were downloaded from BEELINE (Pratapa et al., 2020). 
For single-cell RNA-seq data, the count matrix and metadata of human glioblastoma, human PBMC, and human BMMC were collected from GEO databaset (GSE144623, GSE139369). 
The edgelists generated from multi-omics data were collected from CellOrcle (Kamimoto et al., 2023).

## Qs

### Interpretation of gene clusters? They share topological similarities but what is the significance?

Probably just for validating the method. In practice you can look at it to see if the embedding works.

### How to merge GRNs? 

Seems to be just concatenate two edge lists together.  

### Why project separate networks into one space

To facilitate comparison of network topology change. [Simple network](#Simple%20network) showed that using gene2role, structurally similar genes are closer in the embedding space. Conversely, structurally different genes are far. 

### Why make topological comparisons at all?

Comparing role changes provides additional insight. As [Identification of DTGs between pairwise states](#Identification%20of%20DTGs%20between%20pairwise%20states) shows, sometimes expression level change and topology change do not imply one another.

Also network topology is an important piece of information from network.

### Why not use proximity based embeddings to compare?

As [Simple network](#Simple%20network) showed, proximity based methods cannot accurately capture structural information of genes.