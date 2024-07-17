---
title: CellOracle
theme: solarized
---

# Cell type inference from GRN

---

## Paper overview

[Gene regulatory network](Gene%20Regulatory%20Network.md) (GRN) represents the regulation network of gene expression in cells. Using single cell ATAC and RNA seq data, the authors performed in-silico [transcription factor](Transcription%20Factor.md) (TF) pertubations.

The results are validated in existing data and a new zebrafish model.

---

## Introduction

- Pertubational omics: perturb cell state externally and study the outcome.
- Previous computational approaches require experimental pertubation data for training.
- GRN can be built with unperturbed data, and is more interpretable. The challenge is use the static network to study dynamic cell state change.
- TFs > CellOracle > New cell identity and the trajectory of change

---

## Results

---

### In-silico Pertubation

- The cell identity shift is shown as a vector map of transitions
- Five steps:
	- Cell-type or state specific GRNs are built with [cluster-wise regularized linear regression models](Cluster-wise%20Linear%20Regression.md) with multi-omics data.
	- Shifts in **target gene expression** in response to TF pertubation is calculated. The GRN model is used as a function to propagate the shift in gene expression rather than the absolute gene expression value, representing the signal flow from TF to target gene. The signal is propagated iteratively.
	- Cell identity transition probability is estimated by comparing this shift in gene expression to the gene expression of local neighbors.
	- The transition probability is converted to a **weighted local average vector** to represent the simulated directionality of cell state transition for each cell.
	- Finally, the the multi-dimensional gene expression shift vector is reduced to a two-dimensional (2D) vector

---

### GRN Inference

- [scATAC](scATAC-seq.md) data is used to identify TF binding sites, including [promoter](Promoter.md) and [enhancer](Enhancer.md) regions.
	- [Transcriptional start site (TSS) database](TSS Database) (http://homer.ucsd.edu)
	- Cicero: identifies scATAC-seq [co-accessible peaks](scATAC-seq.md##Co-accessible%20Peaks), which are cell type dependent.
	- DNA sequence of the peaks are scanned for TF binding motifs, consituting the **base GRN structure** of all potential interactions.
	- Using TF information reduces network size and defines **directionality** of the edges.
	- Base GRN for some species are created and shared by the authors

---

- [scRNA](scRNA-seq.md) data is used to identify active connections in the base GRN.
	- Generates the cell-type specific GRN configurations (regulatory relationship and strength) for each cluster.
	- A model is used to predict target gene expression based on TF expression.
	- A regularized linear machine learning model (relatively simple model) is used for network inference.
	- Author comment: this strategy enables the above signal propagation to simulate TF perturbation
	- Certainty of connections is represented as a probability distribution using a Bayesian strategy.
	- Low certainty connections are removed from the base GRN

---

### Validation

A pertubation score is devised that compares the directionality of the pertubation vector to the natural differentiation vector:
	- Positive means same direction; TF KO promotes differentiation
	- Negative means opposite direction; TF KO blocks differentiation

