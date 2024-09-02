# Cell Oracle

#paper
[Github](https://github.com/morris-lab/CellOracle)
Nature [Paper](https://www.nature.com/articles/s41586-022-05688-9#Sec9), 2023 and widely used already
[Tutorial](https://morris-lab.github.io/CellOracle.documentation/)
[Notebooks used for the paper, contain code](https://github.com/morris-lab/CellOracle/tree/master/docs/notebooks)

Washington University School of Medicine in St Louis, St Louis

GRN perturbation: change [Transcription Factor](Transcription%20Factor.md) level and **predict** cell identity shift

## Abstract

Developed CellOracle for [Gene Regulatory Network](Gene%20Regulatory%20Network.md) inference and perturbation analysis. 

Evaluated on mouse and human hematopoiesis, and zebrafish embryogenesis data. The algorithm correctly predicts the outcome of TF knockout and identified additional regulators.

## Method

### Algorithm Overview

CellOracle consists of several steps:
1. **Base GRN** construction using [scATAC-seq](scATAC-seq.md) data or [Promoter](Promoter.md) databases.
2. [scRNA-seq](scRNA-seq.md) data preprocessing.
3. Context-dependent **GRN inference** using scRNA-seq data.
4. Network analysis. Basic [GRN topology Analysis](GRN%20Analysis.md)
5. Simulation of **cell identity** following [Transcription Factor](Transcription%20Factor.md) perturbation.
6. Calculation of the _pseudotime gradient vector field_ and the _inner-product score_ to generate **perturbation scores**.

### Base GRN inference using sc-ATAC data

The base GRN contains _unweighted_, _directional edges_ between a TF and its target gene.

There are two steps, explained below.

CellOracle uses the _regulatory region_'s genomic DNA sequence and TF-binding motifs to construct the base GRN. CellOracle identifies [Regulatory Candidate Genes](Regulatory%20Candidate%20Genes.md) by scanning for TF-binding motifs within the regulatory DNA sequences ([Promoter](Promoter.md) and [Enhancer](Enhancer.md)) of [Open Chromatin Regions](Open%20Chromatin%20Regions.md). 

i.e. look for TF-binding motifs within regulatory DNA sequences within open chromatin regions. The TF-binding motifs are associated with [Regulatory Candidate Genes](Regulatory%20Candidate%20Genes.md).

This steps narrows down the scope of [Regulatory Candidate Genes](Regulatory%20Candidate%20Genes.md) and helps define the directionality of regulatory edges in the GRN.

However, not all TF binding motifs are actively regulating gene expression. [Transcription Regulation](Transcription%20Regulation.md) contain many context-dependent factors. For example, both [Insulator](Insulator.md)s and [Silencer](Silencer.md)s can prevent [Enhancer](Enhancer.md)s and [Promoter](Promoter.md)s from activating transcription. In the next step, [scRNA-seq](scRNA-seq.md) data are used to refine the network.

#### Identification of promoter and enhancer regions

Species and tissue-specific scATAC-seq data, which identify [Open Chromatin Regions](Open%20Chromatin%20Regions.md), are used to find promoter and enhancer regions. 

In the absence of sample/tissue-specific data, using broader scATAC-seq data yields a more general network. This more general network can be fitted to a specific sample using scRNA-seq data during the model fitting process. The final product will consist of context-dependent (cell-type or state-specific) GRN configurations.

**Proximal regulatory DNA elements** are located by locating **TSSs** within the accessible ATAC-seq peaks. This annotation is performed using [HOMER]([http://homer.ucsd.edu/homer/](http://homer.ucsd.edu/homer/)). 

TSS: transcription starting sites, within [Promoter](Promoter.md)s.

**Distal regulatory DNA elements** are obtained using Cicero, a computational tool that identifies [Cis-Regulatory Elements](Transcription%20Regulation.md#Cis-Regulatory%20Elements) on the basis of [Co-Accessibility](Co-Accessible%20Peaks.md), as derived from ATAC-seq peak information. When two ATAC peaks are co-accessible, there is likely some regulatory relationship between them.

Using Cicero, pairs of peaks within 500 kb of each other are identified and calculated a co-accessibility score. Pairs of peaks overlapping a TSS and with a **high co-accessibility score** (>0.8) are identified as distal regulatory elements.

The output is a *bed file* in which all _cis_-regulatory peaks are paired with the target gene name. This bed file is used in the next step. 

CellOracle can also use other input data types to define _cis_-regulatory elements. For example, a database of promoter and enhancer DNA sequences or bulk ATAC-seq data can serve as an alternative if available as a .bed file.

A mouse haematopoiesis base GRN is built with a mouse scATAC-seq atlas consisting of around 100k cells across 13 tissues. This is built into the CellOracle library to support GRN inference when there is none sample-specific scATAC-seq datasets. They also generated general promoter base GRNs for several key organisms commonly used to study _development_, including *10 species and 23 reference genomes*. 

#### Motif scan of promoter and enhancer DNA sequences

CellOracle uses [gimmemotifs]([https://gimmemotifs.readthedocs.io/en/master/](https://gimmemotifs.readthedocs.io/en/master/)) to look for TF binding motifs in each sequence identified above. 

A database for TF binding motifs is required. In this paper they used the gimmemotifs motif v.5 data. CellOracle also provides motif datasets for ten species generated from the [CisBP v.2 database](http://cisbp.ccbr.utoronto.ca/).

CellOracle exports a binary data table to indicate potential connections between a *TF* and a *gene* . It also reports the TF-binding DNA region.

### scRNA-seq data preprocessing

scRNA-seq data need be preprocessed in `Anndata` format. The python library `scanpy` should be used. `Seurat` can also be used. Then the data must be converted to `Anndata` using the CellOracle function `seuratToAnndata`. 

The following steps are performed:
1. filter out zero-count genes by UMI count using `scanpy.pp.filter_genes(min_counts=1)`
2. Normalize by total UMI count per cell `sc.pp.normalize_per_cell(key_n_counts=‘n_counts_all’)`
3. Find **highly variable genes** by `scanpy.pp.filter_genes_dispersion(n_top_genes=2000~3000)`
4. Gene expression is log transformed, scaled, and subjected to dimensional reduction and clustering
5. Non log-transformed gene expression matrix (**GEM**) is also retained for downstream GRN calculation and simulation

### Context-dependent GRN inference using scRNA-seq data

A **regularized linear model** is used to predict target gene expression from regulatory gene expression. The regulatory genes and their corresponding target genes are identified in the previous base GRN construction step. The relationship is shown below: $${x}_{j}=\,\mathop{\sum }\limits_{i=0}^{n}{b}_{i,j}{x}_{i}+\,{c}_{j},$$
where $x_j$ is single target gene expression and $x_i$ is the gene expression value of the [Regulatory Candidate Gene](Regulatory%20Candidate%20Genes.md) that regulates gene $x_j$. $b_{i,j}$ is the coefficient value of the linear model (but $b_{i,j}$ = 0 if $i$ = $j$), and $c$ is the intercept for this model. Here, we use the list of potential regulatory genes for each target gene generated in the [previous base GRN construction step](#Motif%20scan%20of%20promoter%20and%20enhancer%20DNA%20sequences).

$${x}_{i}\in \{{x}_{0},\,{x}_{1},\,\ldots {x}_{n}\}={\rm{Regulatory}}\,{\rm{candidate\; TFs\; of\; gene}}\,{x}_{j}$$

The GEM is first clustered. Then regression is calculated for each cluster. This is called [Cluster-wise Linear Regression](Cluster-wise%20Linear%20Regression.md). This is done because regulatory gene-target gene relationship is non-linear at the whole cell population level, but within each cluster, the cells are more similar to each other, and linear regression has better performance.

[L2 Regularization](L2%20Regularization.md) is applied for the linear model to reduce overfitting. Regularization reduces large coefficients due to overfitting and identifies informative variables. The [Bayesian Ridge Regression](Bayesian%20Ridge%20Regression.md) model or [Bagging Ridge Regression](Bagging%20Ridge%20Regression.md) model are used. Think of them like an advanced linear model that is more robust against overfitting. They also provide the coefficients as a distribution such that the reproducibility of the inferred gene-gene connection can be analyzed. Remember that the coefficient $b$ is estimated. Hence its reliability should be analyzed. Read more about parameter estimation at [MLE vs. Bayesian Parameter Estimation](MLE%20vs.%20Bayesian%20Parameter%20Estimation.md)

In both models, the output is posterior distribution of coefficient value $b$:


$${x}_{j}\sim {\rm{N}}{\rm{o}}{\rm{r}}{\rm{m}}{\rm{a}}{\rm{l}}\,\,(\mathop{\sum }\limits_{i=1}^{n}{b}_{i,j}{x}_{i}+{c}_{j},{\epsilon })$$

$$b\sim {\rm{N}}{\rm{o}}{\rm{r}}{\rm{m}}{\rm{a}}{\rm{l}}\,(\,{\mu }_{b},{{\sigma }}_{b})$$
where $\mu_b$ is the centre of the distribution of $b$, and $\sigma_b$ is the standard deviation of $b$. The normal distribution is defined using mean and standard deviation.

Between the two, Bayesian ridge uses less computational resource. Bagging ridge gives better results.

Using the posterior distribution, one sample t-test (null hypothesis: $b=0$) can be performed for $b$ to calculate its p value. This helps identify robust connections while minimizing connections derived from random noise.

The Bayesian ridge uses the following priors:

$b\sim {\rm{N}}{\rm{o}}{\rm{r}}{\rm{m}}{\rm{a}}{\rm{l}}\,(0,{{\sigma }}_{b})$

${{\sigma }}_{b}^{-1}\sim {\rm{G}}{\rm{a}}{\rm{m}}{\rm{m}}{\rm{a}}\,({10}^{-6},{10}^{-6})$

$b$ is assumed to have a normal distribution centered at 0 with standard deviation $\sigma_b$, while $\sigma_b$ is assumed to have an inverse-[Gamma Distribution](Gamma%20Distribution.md) defined by its two parameters. ${\sigma }_{b}$ is selected to represent **non-informative prior distributions**. This allows the scRNA data to dominate the inference process. Read more at [Non-informative Prior](Bayesian%20Ridge%20Regression.md#Non-informative%20Prior) 

Bayesian ridge uses data in the fitting process to estimate the optimal regularization strength. In the Bagging Ridge model, custom regularization strength can be manually set.

### Simulation of cell identity following perturbation of regulatory genes

After obtaining the GRN, CellOracle simulates how cell identity shifts following perturbation of regulatory genes. The simulated gene expression values are converted into **2D vectors** representing the direction of cell-state transition, a adapting the visualization method previously used by [RNA velocity](https://www.nature.com/articles/s41586-022-05688-9#ref-CR52 "la Manno, G. et al. RNA velocity of single cells. Nature 560, 494–498 (2018).")

The process consists of four steps:
1. data preprocessing
2. signal propagation within the GRN
3. estimation of transition probabilities
4. analysis of simulated transition in cell identity

#### Data preprocessing

Velocyto, a Python package for RNA-velocity analysis ([https://velocyto.org](https://velocyto.org/)) is adapted for the simulation of cell identity. The scRNA-seq data is processed by first filtering the genes then imputing dropouts using [K-nearest Neighbor Imputation](K-nearest%20Neighbor%20Imputation.md), according to Velocyto's requirements.

#### Within-network signal propagation

##### Gradient of the linear model

The linear relationships between target genes and regulatory genes computed in the [previous step](#Context-dependent%20GRN%20inference%20using%20scRNA-seq%20data) is used to predict target gene ($x_j$) expression change following regulatory gene ($x_i$) expression change. A partial derivative $\frac{\partial {x}_{j}}{\partial {x}_{i}}$ is calculated as the _rate of change_. Since the model is linear, the derivative $\frac{\partial {x}_{j}}{\partial {x}_{i}}$ is a constant value and already calculated as $b_{i,j}$ in the previous step if the gene $j$ is directly regulated by gene $i$:

$\frac{\partial {x}_{j}}{\partial {x}_{i}}={b}_{i,j}.$

_That's why they used a linear model - easier derivative._

And we calculate the shift of target gene ${\Delta x}_{j}$ in response to the shift of regulatory gene ${\Delta x}_{i}$:

${\Delta x}_{j}=\frac{\partial {x}_{j}}{\partial {x}_{i}}{\Delta x}_{i}={b}_{i,j}{\Delta x}_{i}$

Indirect connections are accounted for by multiplying the edges to form a composite function of the linear models, which is differentiable accordingly. We apply the _chain rule_ to calculate the partial derivative of the target genes, even between indirectly connected nodes.

$\frac{\partial {x}_{j}}{\partial {x}_{i}}=\mathop{\prod }\limits_{k=0}^{n}\frac{\partial {x}_{k+1}}{\partial {x}_{k}}=\mathop{\prod }\limits_{k=0}^{n}{b}_{k,k+1}$,

where

$\begin{array}{c}{x}_{k}\in \{{x}_{0},\,{x}_{1},\,\ldots {x}_{n}\}\,=\,\text{Gene expression of ordered network}\\ \,\text{nodes on the shortest path from gene}\,i\,\text{to gene}\,j.\end{array}$

For example, when we consider the network edge from gene 0 to 1 to 2, the small shift of gene 2 in response to gene 0 can be calculated using the intermediate connection with gene 1.

$\frac{\partial {x}_{2}}{\partial {x}_{0}}=\frac{\partial {x}_{1}}{\partial {x}_{0}}\times \frac{\partial {x}_{2}}{\partial {x}_{1}}={b}_{0,1}\times {b}_{1,2}$

${\Delta x}_{2}=\frac{\partial {x}_{2}}{\partial {x}_{0}}{\Delta x}_{0}={b}_{0,1}{b}_{1,2}{\Delta x}_{0}$

This way, we focus on the _gradient_ of gene expression equations rather than the _absolute expression values_ so that we do not model the error or the intercept of the model, which potentially includes unobservable factors within the scRNA-seq data.

The calculation above is implemented as vector and matrix multiplication. First, the linear  regression model can be shown as follows.

${X}^{{\prime} }=X\cdot B+C$,

where the $X\in {{\mathbb{R}}}^{1\times N}$ is a gene expression vector containing **$N$ genes**, $C\in {{\mathbb{R}}}^{1\times N}$ is the intercept vector, $B\in {{\mathbb{R}}}^{N\times N}$ is the [Network Adjacency Matrix](Network%20Adjacency%20Matrix.md), and each element $b_{i,j}$ is the coefficient value of the linear model from regulatory gene $i$ to target gene $j$.

##### Perturbation propagation

First, we set the perturbation input vector $\Delta {X}_{{\rm{input}}}\in {{\mathbb{R}}}^{1\times N}$, a sparse vector consisting of zeros except for the perturbed gene $i$. For the perturbed gene, we set the shift of the TF to be simulated. The CellOracle function will produce an error if the user enters a gene shift corresponding to an out-of-distribution value.

> [!note]
> The calculation is done for each cell. Hence the input vector has 1 row and N columns matching N genes in the cell.

Next, we calculate the shift of the first target gene. The change then propagates down the GRN:

$\Delta {X}_{{\rm{simulated}},n=1}=\Delta {X}_{{\rm{input}}}\cdot B$.

However, we **fix** the perturbed gene $i$ value, and the ${\Delta x}_{i}$ retains the same value as the input state. Thus, the following calculation will correspond to both the first and the second downstream gene shift calculations. 

$\Delta {X}_{{\rm{simulated}},n=2}=\Delta {X}_{{\rm{simulated}},n=1}\cdot B$.

Likewise, the recurrent calculation is performed to propagate the shift from gene to gene in the GRN. Repeating this calculation for $n$ iterations, we can estimate the effects on the first to the $n_{th}$ indirect target gene:

$\Delta {X}_{{\rm{simulated}},n}=\Delta {X}_{{\rm{simulated}},n-1}\cdot B$.

In each of the calculation above, the respective coefficients between the input and output genes in $B$ are used for calculation. CellOracle performs **three** iterative cycles in the default setting, sufficient to predict the directionality of changes in cell identity. Higher numbers can lead to errors. 

Of note, CellOracle performs the calculations cluster-wise after splitting the whole GEM into **gene expression submatrices** on the basis of the assumption that each cluster has a unique GRN configuration. Remember that the linear relationships were also computed after clustering the GEM into clusters. Each cluster has a different linear relationship.

Also, gene expression values are checked between each iterative calculation to confirm whether the simulated shift corresponds to a _biologically plausible range_. If the expression value for a gene is negative, this value is adjusted to zero.

#### Estimation of transition probabilities

Using the simulated gene expression shift vector $\Delta {X}_{{\rm{simulated}}}\in {{\mathbb{R}}}^{1\times N}$ after TF perturbation, CellOracle calculates the probabilities of cell identity transition. Then it projects the directionality of cell identity transition onto the dimensional reduction embedding, visualized as arrows pointing in the direction of cell identity shift.

> [!info]
> For this task, CellOracle uses a similar approach to [Velocyto](https://github.com/velocyto-team/velocyto.py). Velocyto visualizes future cell identity on the basis of the RNA-splicing information and calculated vectors from RNA synthesis and degradation differential equations. CellOracle uses the simulated gene expression vector $\Delta {X}_{{\rm{simulated}}}$ instead of RNA-velocity vectors.

First, CellOracle estimates the cell transition probability matrix $P\in {{\mathbb{R}}}^{M\times M}$ ($M$ is number of cells): $p_{ij}$, the element in the matrix $P$, is defined as the probability that cell $i$ will adopt a similar cell identity to cell $j$ after perturbation. To calculate $p_{ij}$, CellOracle calculates the Pearson’s correlation coefficient between $d_i$ and $r_{ij}$:

${p}_{ij}=\frac{\exp \left(corr\left({r}_{ij}{,d}_{i}\right)/T\right)}{\sum _{j\in G}\exp \left(corr\left({r}_{ij}{,d}_{i}\right)/T\right)}$,

where $d_i$ is the simulated gene expression shift vector $\Delta {X}_{{\rm{simulated}}}\in {{\mathbb{R}}}^{1\times N}$ for cell $i$, and ${r}_{ij}\in {{\mathbb{R}}}^{1\times N}$ is a subtraction of the gene expression vector $X\in {{\mathbb{R}}}^{1\times N}$ between cell $i$ and cell $j$ in the original GEM. The value is normalized by the [Softmax](Softmax.md) function (default temperature parameter $T$ is 0.05). The calculation of $p_ij$ uses neighboring cells of cell $i$. The KNN method selects local neighbors in the dimensional reduction embedding space (_k_ = 200 as default).

> [!note]
> Pearson correlation measures how similar the simulated gene expression shift vector is with the actual gene expression difference. The Softmax function first exponentiate the correlation value (call it $r$ for now), making the difference larger then divide $r$ by the total $r$ for all the cells. This way a probability to shift to cell $i$ is calculated. The total number of neighboring cells is 200. $G$ refers to these cells.

> [!note] KNN
> Just like [K-nearest Neighbor Imputation](K-nearest%20Neighbor%20Imputation.md), the KNN method to select neighbors is based on a chosen distance metric. The closest 200 neighbors are selected to calculate the transition probabilities of cell $i$ to them.

#### Calculation of simulated cell-state transition vector

With the transition probability matrix $P$, the direction of cell identity shift can be plotted on the dimension reduced plot.

> [!note] Dimension Reduction
> They recommend force directed graph as the dimension reduction method. An alternative when there are too many overlapping branches is UMAP.

CellOracle calculates the local **weighted average** of vector ${V}_{i,j}\in {{\mathbb{R}}}^{1\times 2},{V}_{i,j}$ denotes the 2D vector obtained by subtracting the 2D coordinates in the dimensional reduction embedding between cell $i$ and cell $j$ $({\rm{cell}}\;j\in G)$.

${V}_{i,{\rm{s}}{\rm{i}}{\rm{m}}{\rm{u}}{\rm{l}}{\rm{a}}{\rm{t}}{\rm{e}}{\rm{d}}}=\,\sum _{j\in G}{p}_{ij}{V}_{i,j}$

${V}_{i,{\rm{simulated}}}$ is the simulated 2D cell identity shift vector. 

> [!note] Why is it Weighted Average
> Imagine two vectors going from the origin. If you subtract one from the other, you get the vector that connects the tips of both. This difference is then scaled by the transition probability and summed. 
> 
> Remember that in the Softmax function, the probability is obtained by dividing by the **total** exponentiated Pearson correlation. The probabilities are the weights that makes ${V}_{i,{\rm{simulated}}}$ a **weighted average**.

#### Calculation of vector field

It is hard to visualize the vectors for each cell in a reasonably large graph. A grid, ${V}_{{\rm{vector}}{\rm{field}}}=\,{{\mathbb{R}}}^{2\times L\times L}$, is defined for the plot. $L$ is grid number, default $L$ is 40. Then for each grid point, ${v}_{{\rm{grid}}}\in {{\mathbb{R}}}^{2}$, an element in the ${V}_{{\rm{vector}}{\rm{field}}}$, the nearby vectors are averaged using [Gaussian Kernel Smoothing](Gaussian%20Smoothing.md).

> [!note] Gaussian Smoothing
> Gaussian smoothing does a weighted average for all the vectors in the window using weight defined by a Gaussian distribution.


${v}_{{\rm{grid}}}={\sum }_{i\in H}{K}_{\sigma }(g,\,{V}_{i,{\rm{simulated}}}){V}_{i,{\rm{simulated}}}$,

where the $g\in {{\mathbb{R}}}^{2}$ denotes _grid point coordinates_, $H$ is the neighbor cells of $g$, and ${K}_{\sigma }$ is the Gaussian kernel weight. The higher the distance between the vector and the grid point, the smaller the weight:

${K}_{\sigma }({v}_{0},{v}_{1})=\exp \left(\frac{-{\parallel {v}_{0}-{v}_{1}\parallel }^{2}}{2{\sigma }^{2}}\right)$.

This way each grid has a vector that is the weighted average of nearby vectors. The whole trend can be visualized much more easily.

> [!note] Symbols
> $N$: the number of genes
> $M$: the number of cells
> $G$: group of neighboring cells of cell $i$
> $B$: the network adjacency matrix
> $g$: grid points

### Calculation of pseudotime gradient vector field and inner-product score to generate a perturbation score

[Pseudotime](6.%20时空组学拟时序分析.md) is an analysis technique of single cell/spatial RNA sequencing data. It infers the developmental trajectory from the gene expression in the cells that come from a common origin. For example, how neural cells develop into each other can be studied using pseudotime analysis.

To aid the interpretation of CellOracle's simulation of identity shift, pseudotime analysis is done for the data. The result is then converted into a grid of vectors like the cell identity shift result. We quantify the similarity between the differentiation vector fields and KO simulation vector fields by calculating their inner-product value, which we term the **perturbation score** (PS)

#### Differentiation pseudotime calculation

Differentiation pseudotime is calculated using DPT, a diffusion-map-based pseudotime calculation algorithm, using the scanpy.tl.dpt function. Other methods such as _Monocle_ and _URD_ also work with CellOracle.

#### Differentiation vector calculation based on pseudotime data

The pseudotime data are transferred to the _n_ by _n_ 2D grid points (_n_ = 40 as default). Two methods are implemented: KNN regression and polynomial regression (add notes later). 

> [!info] Choice of Method
> Polynomial regression should be used when the developmental branch is relatively simple bifurcation. KNN regression should be used when the branching is more complex.

The gradient of pseudotime data on the 2D grid points are calculated using the numpy.gradient function, producing the 2D vector map representing the _direction of differentiation_.

#### Inner-product value calculation between differentiation and KO simulation vector field

The inner product is calculated between the two matrices to get PS (-1 to 1). A positive PS (green) means that perturbation __promotes__ differentiation, while a negative PS means perturbation __represses__ differentiation. 

> [!note] KO Simulation
> In a knockout (KO) simulation, if the PS is positive, it means removing the TF promotes differentiation. Hence the TF itself inhibits differentiation. If the PS is negative, it means the TF promotes differentiation.

#### PS calculation with randomized GRN model to calculate PS cut-off value

CellOracle produces randomized GRN models to calculate a cutoff value for negative PS in TF KO simulations.

1. A random GRN is generated (randomized $B$)
2. A randomized simulation vector ($\Delta X_\text{input}$ from [Perturbation propagation](#Perturbation%20propagation)) is used to calculate PS. 
3. The PS from random GRN forms the null distribution. Then the cut-off value is chosen from the 99% percentile of the null distribution.

> [!note] FPR
> The 99% percentile is chosen to have a low [False Positive Rate (FPR)](Confusion%20Matrix.md#False%20Positive%20Rate%20(FPR)). At 99% percentile, the FPR is 0.01. FPR refers to the proportion of negative cases (in this case negative PS due to random chance) that are labeled as positive (in this case negative PS is caused by the TF promoting differentiation). Only the negative scores lower than the threshold are labeled as positives.
> 
> Why not set the threshold to the minimum of randomized PS? Because the minimum value can be very low due to random chance. It will reduce FPR to minimum, but can reduce [True Positive Rate (TPR) / Sensitivity / Recall](Confusion%20Matrix.md#True%20Positive%20Rate%20(TPR)%20/%20Sensitivity%20/%20Recall). Furthermore, the randomization can vary the minimum greatly, which is not good for reproducibility, while the 99% percentile is more stable for a distribution.

#### Focus on one development branch

CellOracle enables analysis of one development branch. See their official tutorial.

### Network Analysis

CellOracle can do standard [GRN Analysis](GRN%20Analysis.md) like [Network Topology Metrics](Network%20Topology%20Metrics.md) and module analysis. Before the analysis, weak connections need to be filtered out. The criteria can be defined by the user.

CellOracle uses [igraph]([https://igraph.org](https://igraph.org/)) for this step.

### Choice of dimensionality reduction method

For the force-directed graph calculation, we recommend using Scanpy’s sc.pl.draw_graph [function](https://www.nature.com/articles/s41586-022-05688-9#ref-CR59 "Wolf, F. A., Angerer, P. & Theis, F. J. SCANPY: large-scale single-cell gene expression data analysis. Genome Biol. 19, 15 (2018).") or [SPRING](https://www.nature.com/articles/s41586-022-05688-9#ref-CR60 "Weinreb, C., Wolock, S. & Klein, A. M. SPRING: a kinetic interface for visualizing high dimensional single-cell expression data. Bioinformatics 34, 1246–1248 (2018)."). Both internally use force atlas 2 (ref. [61](https://www.nature.com/articles/s41586-022-05688-9#ref-CR61 "Jacomy, M., Venturini, T., Heymann, S. & Bastian, M. ForceAtlas2, a continuous graph layout algorithm for handy network visualization designed for the Gephi software. PLoS ONE 9, e98679 (2014).")). Compared to UMAP, force-directed graphs can capture more fine-branching structures but can be unstable if the data have many branches that can overlap. To avoid branch overlap, PAGA cell trajectory information can be used to initiate the force-directed graph calculation: [https://scanpy.readthedocs.io/en/stable/tutorials.html#](https://scanpy.readthedocs.io/en/stable/tutorials.html#)[https://github.com/theislab/paga](https://github.com/theislab/paga).

We recommend using force-directed graphs as a first choice because they generally produce a high-resolution lineage structure. However, we recommend UMAP as a reliable alternative if overlapping branches are observed. In our CellOracle tutorial, we show the detailed guide and code for the dimensionality reduction implementation, including data preprocessing: [https://morris-lab.github.io/CellOracle.documentation](https://morris-lab.github.io/CellOracle.documentation).

## Data

All data, including sequencing reads and single-cell expression matrices, are available from the GEO under accession codes [GSE72859](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE72859) (ref. [16](https://www.nature.com/articles/s41586-022-05688-9#ref-CR16 "Paul, F. et al. Transcriptional heterogeneity and lineage commitment in myeloid progenitors. Cell 163, 1663–1677 (2015).")), [GSE112824](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE112824) (ref. [32](https://www.nature.com/articles/s41586-022-05688-9#ref-CR32 "Farrell, J. A. et al. Single-cell reconstruction of developmental trajectories during zebrafish embryogenesis. Science 360, eaar3131 (2018).")) and [GSE145298](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE145298) for the zebrafish profiling from this study; and from ArrayExpress under accession codes [E-MTAB-7325](http://www.ebi.ac.uk/microarray-as/aer/result?queryFor=Experiment&eAccession=E-MTAB-7325) (_Tal1_−/− chimeras) and [E-MTAB-7324](http://www.ebi.ac.uk/microarray-as/aer/result?queryFor=Experiment&eAccession=E-MTAB-7324) (wild-type chimeras). Simulations can be explored at [https://celloracle.org](https://celloracle.org/).