# Cell Oracle

#paper
[Github](https://github.com/morris-lab/CellOracle)
Nature [Paper](https://www.nature.com/articles/s41586-022-05688-9#Sec9), 2023 and widely used already

Washington University School of Medicine in St Louis, St Louis

[Gene Regulatory Network](Gene%20Regulatory%20Network.md) inference with SCENIC+
GRN perturbation: change [Transcription Factor](Transcription%20Factor.md) level and **predict** cell identity shift

## Abstract

Developed CellOracle for GRN inference and perturbation analysis. 

Evaluated on mouse and human hematopoiesis, and zebrafish embryogenesis data. The algorithm correctly predicts the outcome of TF knockout and identified additional regulators.

## Method

### Algorithm Overview

CellOracle consists of several steps:
1. **Base GRN** construction using [scATAC-seq](scATAC-seq.md) data or [Promoter](Promoter.md) databases.
2. [scRNA-seq](scRNA-seq.md) data preprocessing.
3. Context-dependent **GRN inference** using scRNA-seq data.
4. Network analysis. [GRN Analysis](GRN%20Analysis.md)?
5. Simulation of **cell identity** following [Transcription Factor](Transcription%20Factor.md) perturbation.
6. Calculation of the _pseudotime gradient vector field_ and the _inner-product score_ to generate **perturbation scores**.

### Base GRN inference using sc-ATAC data

The base GRN contains _unweighted_, _directional edges_ between a TF and its target gene.

CellOracle uses the _regulatory region_'s genomic DNA sequence and TF-binding motifs for this task. CellOracle identifies [Regulatory Candidate Genes](Regulatory%20Candidate%20Genes.md) by scanning for TF-binding motifs within the regulatory DNA sequences ([Promoter](Promoter.md) and [Enhancer](Enhancer.md)) of [Open Chromatin Regions](Open%20Chromatin%20Regions.md). 

i.e. look for TF-binding motifs within regulatory DNA sequences within open chromatin regions. The TF-binding motifs are associated with [Regulatory Candidate Genes](Regulatory%20Candidate%20Genes.md).

This steps narrows down the scope of [Regulatory Candidate Genes](Regulatory%20Candidate%20Genes.md) and helps define the directionality of regulatory edges in the GRN.

