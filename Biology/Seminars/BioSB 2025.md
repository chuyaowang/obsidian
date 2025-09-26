# BioSB 2025

#seminar 

## Dynamics of spinal cords development

 >Frank Cricks institute
 >Developmental biology
 
 - Question: what where when of developmental biology
 - Answer
	 - What genes to mutate
	 - Single cell pseudotime trajectory
 - Marr's 3 levels of analysis for analysis of developmental biology
	 - computational: spatial gene expression
	 - algorithmic:  morphogen gradient
	 - implementational: gene regulatory network

### Dynamics of cell fate decisions

- scRNA
- infer pseudotime trajectory
- snapshot inferences
- need more: how gene expression change in time in sc resolution > time resolved transcriptomics
	- label new transcripts with metabolite
	- know which new transcripts form over time

### sci-FATE2.0


### Example: differentiation of spinal cord

- obtained time resolved transcriptomics
- modeling the data: a biophsical data
	- $v=\alpha -yx$ transcripton rate - degradation rate
	- another eqn
		- infer the velocity
- Exploiting data structure for velocity inference
	- genetic structure
	- cell structure
	- VAE approach: called Velvet. outputs low dimensional representation of cellular differentiation process
- Extend: model dynamics of individual genes: Fokker Planck equation. Model brownian motion
- Simulate cell fate dynamics: vector field of differentiation

### Cell fate decisions

- Nodes: cell states
- Edges: decisions and transitions
- Waddington landscape: differentiation of cell as a ball roling in a valley
	- can we make a quantitative landscape
- Dynamical landscape: 
	- attractors: cell types, bottom of valleys
	- potential function: height of the landscape
	- devise mathematical description
	- parameter of the equation can be changed and it changes the landscape
	- Catastrophe theory
- Differentiating ES cells: can be differentiate into 5 cell types, biomarkers to know which cell type
	- FACS analysis
	- Quantifying cell identity
	- Build landscape to describe cell fate decision: build a topology
	- Catastrophe theory identifies possibilities that fits the cell differentiation pattern
	- Parameterize the landscape
	- Fitting the landscape to experimental data
- Application
	- Simulate experimental conditions that are not actually measured
	- Make prediction and use experiment to confirm
	- Simulate sequential change of experimental condition in time
		- predict how cell state rolls through the valley in time
		- what if a condition lasts shorter time

### Summary

- Extend to scRNA-seq
- 3 types of maps:
	- cell histology
	- gene expression dimension (like umap)
	- cell state landscape (the valley analogy)
	- underlying: molecular mechanism

## multimodal single cell level spatial integration

> Roy Lardenoije
> TU Delft

- Spatial transcriptomics
	- single cell level resolution
	- location in the tissue
	- no histopathology: ex. cytoxoxic amyloiad plaque  in a tissue section
- Amyloid pathology
	- AD
	- Aggregation due to protein misfolding
	- Similar pathology is observed in T2DM
	- Pathology: death of parenchymal cells, migration of cells involvedin fibrosis, immune cell activation
- Goal: determine the impact of amyloid proximity on cell type composition and ge profiles in t2dm and ad tissue. cross-followed by tissue study
- Spatial transcriptome data collection
- Amyloid staining -> histopathology
- Registration of modalities: combine gene expression and staining
- Pathology annotation of cells
- Cell type prediction
	- RCTD: robust cell type decomposition: uses refernece scRNA-seq snRNA seq data
	- cell type composition comparison
- Clustering
- Differential gene expression for close-to-pathology tissue

## Independent scaling factor normalization: normalizing sequencing based single cell protein count data

> Tim Stohn
> VU

- single cell protein count data measures AB attached nucleotide sequences
- assumptions from scRNA seq do not hold true for single cell prtein data
- CLR (center log transform) normalized data contains many protein correlations
	- how can we validate these correlations without ground truth

### Normalization and correlation

- measured data is a subset of the true proteome
- assumption: detection efficiency is independent of protein counts
- normalization strategy should align with this assumption: normalization factor is independent of protein composition

### What normalization factor to use?

- in log space: normalization factors are additive $N=M+\beta$
- $cov(M_{i},M_{j})$

### ISFaN normalizes by keeping the variance pattern stable

- does not introduce spurious correlations

## Interpretable metric of clustering in spatial arrangement of immune cells

> Radbound
> 

- Immune cell distribution in tumor tissue
- Types of immune cells distribute in space
- Spatial statistics:
	- point parrern representation
	- dispersion
	- randomness
	- clustering
	- spatial pattern depends on scale: clustered at small scale, dispersed at large
- Immune cells have highe diversity in clustering
- We want a metric to quantify spatial distribution that
	- scale dependent, a function of distance
	- can distinguish of dispersion, randomness, clustering
	- can quantify the degree of clustering
	- interpretable and easy to use
- Ripley's K-function: detects deviation from randomness
	- cannot be interpreted as a degree of clustering
	- need to develop new function
- A metric can be interpreted as degree of clustering if
	- Between -1 and 1 for all R
	- -1 for maximal dispersion
	- asymtotically 0 for complete spatial randomness
	- 1 for maximal clustering
- a ppint pattern is maixmally clustered if at a small distance it does not add a neighbor
- a - is maximal dispersed if it has no neighbor at a small distance
- despersion rnadomness and clustering can be disinguished by comapring the number of neighbors at two scales
- Developed: local correlation function
- A bandwidth free local correlation function that removes h

## Interpretable ML meets multiscale omics

> TU Delft

- ML appkcations
	- precision medicine for oncology
	- multimodal atlases
- precision medicine for oncology
	- DNA repair deficiency
	- tumor vulnerability
- multimodal atlases
	- link modalities and learn models
		- coordinate: spatial data
		- functional: genes encode for proteins
		- entity: bulk/spatial/single cell transcriptomics
	- interpretability
- interpretability
	- statistical model of phenomena: high interpretability
	- ML model: less explainable, need XAI
		- supervised model can be explained by tools: SHAP, LIME, many more
		- unsupervised model: how to explain the latent embeddings?
- explain latent dimension
	- latent dimensioi: capture local latent structure in data, organized in lower dimensional space
	- model decision y are contained in the relative local organization of the data
	- organization can be linked to input features X for reasoning about model decisions
- LAVA: locality aware variable associations
	- define localities focus on logal organization
	- link to original data explain organization via within locality correlations between features in original data belonging to the locality
	- reveal shared sub-patterns across localities

## Inferring common evolutionary trajectories using posets

- tumor evolution: order of mutation happening matters for tumor severity and disease onset time and drug response
- Challenges:
	- infinite sites assumption: aech label occurs onlyone time
	- uncertainties: uncertain in part of the tree
	- tumor heterogeniety
- Posets: partially ordered sets: consist of ordered and unordered components
- Common induced trajectories (CIT):

## Studying brain disorder heterogeneity using genetic susceptibility

- Brain disorder heterogeneity
- Netherlands Brain Bank: brain sample from various brain disorders and data
- GSA array data + testing for individual mutations
- Genome wide association study: identify variants increase disease risk
- Polygenic risk for different brain disorders in this post-mortem cohort
- Heterogeneity: why do some patients have a higher risk for another disease than their disease?

## TDCC-LSH 

- Funding for projects

## Exposomics: where systems biology meets chemistry

- [Slides](https://zenodo.org/records/15470416)
- Exposome: total chemicals one is exposed to
- The exposome contains many chemical classes: drugs, pesticides, amino acids, etc.
- Dynamic range is way out of instrument range
- PubChem: largest public chemical database 
- MassBank: mass spectra library
- Targeted analysis: instead of all chemicals, measure only a region of interest
- PubChemLite