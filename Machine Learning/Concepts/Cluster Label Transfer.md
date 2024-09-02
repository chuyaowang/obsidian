# Cluster Label Transfer

**Cluster-label transfer** is a computational technique used in [scRNA-seq](scRNA-seq.md) and [scATAC-seq](scATAC-seq.md) studies to map and compare cell clusters identified in one dataset to another dataset. 

It involves transferring the labels (or identities) of clusters from a reference dataset (where cell types or states have already been annotated) to a target dataset (where these annotations are not yet known).

## Purpose of Cluster-Label Transfer

1. **Identification of Similar Cell Populations:**
   - Cluster-label transfer helps in identifying and annotating similar cell populations across different datasets, conditions, or experiments. It allows researchers to recognize if a particular cell state or cluster observed in one dataset is present in another.

2. **Consistency and Validation:**
   - By comparing clusters between datasets, researchers can validate the presence of specific cell states and ensure that findings are consistent across different experimental conditions or biological replicates.

3. **Characterization of Cell States:**
   - This technique helps in characterizing new or unknown cell states by leveraging information from well-annotated reference datasets. It provides insights into the functions and characteristics of cell clusters in the target dataset.

## Steps

1. **Pre-processing:**
   - **Data Normalization:** Both the reference and target single-cell datasets are normalized to ensure comparability.
   - **Feature Selection:** Highly variable genes or features are selected for downstream analysis to capture the most informative aspects of the data.

2. **Dimensionality Reduction:**
   - Techniques such as Principal Component Analysis (PCA) are applied to reduce the dimensionality of the data while retaining the most important features.
   - This step is performed on both the reference and target datasets to facilitate alignment.

3. **Integration and Alignment:**
   - **Shared Space Mapping:** Methods like Canonical Correlation Analysis (CCA) or mutual nearest neighbors (MNN) are used to align the reference and target datasets in a shared low-dimensional space.
   - **Batch Effect Correction:** Techniques such as Harmony or Seurat’s integration are employed to correct for batch effects and technical differences between datasets.

4. **Cluster Identification in Reference Dataset:**
   - Clustering algorithms (e.g., Louvain or Leiden) are used to identify distinct cell clusters in the reference dataset.
   - These clusters are annotated based on known cell types, states, or conditions.

5. **Label Transfer:**
   - **Nearest Neighbor Search:** For each cell in the target dataset, the nearest neighbors in the reference dataset are identified based on their positions in the shared low-dimensional space.
   - **Label Assignment:** The cluster labels from the nearest neighbors in the reference dataset are transferred to the corresponding cells in the target dataset. Majority voting or probabilistic methods are used to assign the most likely label to each cell.

6. **Validation and Fine-Tuning:**
   - The transferred labels are validated by comparing the expression patterns of known marker genes in both the reference and target datasets.
   - Fine-tuning may involve re-clustering the target dataset with the transferred labels as initial conditions to refine the cluster assignments.

## Tools and Algorithms

Several computational tools and algorithms are commonly used for cluster label transfer:

1. **Seurat:**
   - The Seurat package in R includes functions for data normalization, dimensionality reduction, integration, and label transfer. The `FindTransferAnchors` and `TransferData` functions facilitate label transfer between datasets.

2. **Scanpy:**
   - The Scanpy package in Python also supports integration and label transfer. Functions like `scanpy.pp.neighbors` and `scanpy.tl.ingest` are used for these purposes.

3. **Liger:**
   - Liger (Linked Inference of Genomic Experimental Relationships) is another tool that integrates single-cell datasets and supports label transfer.

## Why the Authors Used Cluster Label Transfer

In the context of the [study](Single-cell%20ATAC%20and%20RNA%20sequencing%20reveal%20pre-existing%20and%20persistent%20cells%20associated%20with%20prostate%20cancer%20relapse.md) on enzalutamide (ENZ) resistance in prostate cancer:

1. **Identification of Consistent Cell States:**
   - The authors aimed to identify and validate specific cell clusters associated with ENZ resistance across different datasets. By transferring cluster labels from a well-annotated reference dataset to other datasets, they ensured that the identified cell states were consistently observed.

2. **Validation Across Models:**
   - Using cluster label transfer allowed the authors to validate that the ENZ-resistant cell states observed in one model (e.g., LNCaP-derived RES-A and RES-B cells) were also present in other independent models and conditions (e.g., LNCaP-ENZ168 and RES-C cells).

3. **Robustness of Findings:**
   - By confirming the presence of resistant cell clusters in multiple datasets, the authors strengthened the robustness and generalizability of their findings. This approach provided confidence that the observed mechanisms of resistance were not artifacts of a single experimental setup.

### Methods used

   - **Integrated Clustering:** The authors first performed integrated clustering of scRNA-seq data from different samples (e.g., LNCaP parental, ENZ-resistant models RES-A, and RES-B) to identify distinct cell clusters.
   - **Label Transfer:** They then transferred these cluster labels to independent scRNA-seq datasets, such as LNCaP ENZ-treated for one week (LNCaP-ENZ168) and an independent ENZ-resistant LNCaP-derived cell line (RES-C).

### Findings

   - The label-transfer process confirmed the presence of initial, persistent, and ENZ-induced clusters in independent datasets. This demonstrated that specific cell states associated with ENZ resistance were consistently observed across different models, reinforcing the robustness of their findings.

### Implications

   - **Validation of Resistant States:** The consistent identification of resistant cell states across different datasets validated the relevance of these states in ENZ resistance.
   - **Generalizability:** The findings suggested that the mechanisms driving ENZ resistance were not restricted to a single cell line or experimental condition but were generalizable to other prostate cancer models.
   - **Therapeutic Insights:** Understanding these consistent cell states can provide insights into potential therapeutic targets and strategies to overcome resistance in prostate cancer.

## Why didn't they do it for sc-ATAC data

Cluster label transfer can be more **challenging** for single-cell ATAC-seq (scATAC-seq) data compared to single-cell RNA-seq (scRNA-seq) data due to several reasons:

1. **Data Characteristics:**
   - **Sparse Data:** scATAC-seq data is inherently [Sparse](Sparsity.md) because only a small fraction of the genome is accessible and captured in each cell. This sparsity makes it difficult to identify robust clusters and transfer labels reliably.
   - **Different Signal Types:** scATAC-seq measures chromatin accessibility, which is a different type of signal compared to gene expression measured by scRNA-seq. The regions of open chromatin are fewer and more variable, complicating direct label transfer.

2. **Lack of Established Reference Maps:**
   - **Reference Datasets:** There are fewer well-annotated reference datasets for scATAC-seq compared to scRNA-seq. Without robust reference maps, it becomes challenging to perform reliable label transfer.
   - **Complexity of Chromatin States:** The chromatin landscape is highly dynamic and context-dependent, which means that chromatin accessibility profiles can vary widely between different cell types and conditions.

3. **Computational Tools and Methods:**
   - **Tool Availability:** While there are many tools and methods available for integrating and transferring labels in scRNA-seq data, the computational methods for scATAC-seq are still developing. Tools like Seurat and Scanpy are primarily designed for scRNA-seq data.
   - **Integration Challenges:** Integrating scATAC-seq data with scRNA-seq data or other scATAC-seq datasets requires sophisticated methods to align different data modalities, which can be computationally intensive and complex.

### Alternative Approaches Used

Instead of cluster label transfer, the authors might have used other methods to analyze and validate their scATAC-seq data:

1. **Independent Clustering:**
   - The authors likely performed independent clustering of the scATAC-seq data to identify distinct chromatin accessibility profiles within the dataset.
   - This approach allows them to characterize the unique features of chromatin accessibility without relying on external labels.

2. **Integration with scRNA-seq Data:**
   - The authors might have integrated scATAC-seq data with scRNA-seq data to correlate chromatin accessibility with gene expression profiles. Techniques like joint embedding or linked analysis can help map the relationships between chromatin states and transcriptional programs.
   - This integration can provide insights into how changes in chromatin accessibility influence gene expression and contribute to drug resistance.

3. **Functional Validation:**
   - The authors could have validated their findings through functional assays, such as identifying differentially accessible regions (DARs) and linking them to gene regulatory elements.
   - By performing functional validation, they can ensure that the observed chromatin accessibility changes have biological significance and are relevant to the study's goals.

### Specific Context in the Study

1. **Focus on scRNA-seq for Label Transfer:**
   - In the study on enzalutamide resistance, the authors might have focused on scRNA-seq data for cluster label transfer because gene expression profiles are more directly interpretable and easier to compare across different conditions.
   - The scRNA-seq data provides a more straightforward way to identify and validate cell states associated with drug resistance.

2. **Characterizing Chromatin Reprogramming:**
   - For the scATAC-seq data, the primary goal might have been to characterize the chromatin reprogramming events underlying resistance. This involves identifying regions of differential accessibility and linking them to transcription factor binding sites and regulatory elements.
   - The authors might have used scATAC-seq data to provide a complementary layer of information that supports the findings from scRNA-seq analysis.
