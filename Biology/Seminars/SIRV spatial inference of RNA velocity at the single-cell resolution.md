# SIRV spatial inference of RNA velocity at the single-cell resolution

#paper 
[link](https://academic.oup.com/nargab/article/6/3/lqae100/7728020)

## 1. Motivation

The authors were driven by the need to study cellular differentiation dynamics **in situ**—that is, within the spatial context of tissues. Traditional single-cell RNA sequencing (scRNA-seq) captures the transcriptomic state of dissociated cells but loses information on their physical locations and microenvironment cues. At the same time, although RNA velocity methods (which estimate the future state of cells based on spliced and unspliced mRNA ratios) have provided valuable insights into differentiation, spatial transcriptomics platforms typically lack the capability to capture both spliced and unspliced mRNA at high resolution. This gap motivated the development of a method to integrate spatial data with scRNA-seq so that one could infer “spatial RNA velocity”—thereby uncovering how cells progress along differentiation trajectories within their native tissue architecture.

---

## 2. Research Question

The paper addresses the question:  
**How can one infer and visualize RNA velocity, and hence differentiation trajectories, directly in the spatial context, using high-resolution spatial transcriptomics data that is enriched with spliced and unspliced mRNA information from reference scRNA-seq data?** 

This is accomplished by overcoming current limitations in spatial methods that do not natively provide the kinetic signal (spliced/unspliced counts) necessary for RNA velocity analysis.

---

## 3. Relevant Background Information

To set the stage for their innovation, the authors draw on several strands of background research:

- **Single-Cell RNA Sequencing (scRNA-seq):**  
  scRNA-seq has revolutionized our ability to characterize cell states and infer differentiation trajectories. However, it provides only static snapshots and loses the spatial arrangement of cells.

- **RNA Velocity:**  
  Introduced by La Manno et al., RNA velocity uses the balance between unspliced (immature) and spliced (mature) mRNA to predict the future state of a cell. This dynamic measure gives insight into the direction and speed of cellular transitions, making it a powerful tool in inferring developmental trajectories.

> [!info]- How can scRNA differentiate spliced and unsplice mRNA
> Single‐cell RNA sequencing (scRNA‐seq) protocols are designed in a way that the resulting sequence reads can be computationally classified as coming from either mature (spliced) mRNA or immature (unspliced) precursor mRNA. Here’s how that differentiation happens:
> 
> 1. **Library Preparation and Priming:**  
>    Many scRNA‐seq protocols use oligo‐dT priming to target polyadenylated RNAs. Both mature mRNAs and many nascent pre-mRNAs in the nucleus carry poly-A tails; however, they differ in their structure. Mature mRNA is fully processed, meaning its introns have been excised so that its sequence is composed exclusively of exonic regions. In contrast, unspliced RNA typically retains intronic sequences along with its exons.
> 
> 2. **Sequencing and Read Mapping:**  
>    Once the RNA is converted to cDNA and sequenced, the reads are aligned to a reference genome or transcriptome. Critical to this step is the use of detailed gene annotations that indicate the positions of exons (coding sequences) and introns.  
>    - **Spliced Reads:** Reads that map entirely to annotated exon regions (or across exon–exon junctions) are classified as deriving from mature, spliced mRNA.  
>    - **Unspliced Reads:** Reads that either span intron–exon boundaries or map predominantly to intronic regions indicate that they originate from unspliced, or partially processed, precursor transcripts.
> 
> 3. **Computational Tools and Pipelines:**  
>    Software pipelines such as Velocyto, kallisto with BUStools, or STARsolo are designed to analyze the alignment of individual reads in the context of gene models. They use the following strategies:
>    - **Annotation Lookup:** Each read is checked against the gene annotation. If a read falls within an intronic region (or overlaps an exon–intron junction without covering two exons), it is flagged as unspliced.  
>    - **Exon-Only Confirmation:** Reads that cover sequences known to be present only in mature mRNA are classified as spliced.
>    - **UMI Deduplication:** Unique Molecular Identifiers (UMIs) help in avoiding counting PCR duplicates, ensuring that the counts for spliced versus unspliced transcripts are as accurate as possible.
> 
> 4. **Outcome and Applications:**  
>    The result of this process is two separate count matrices—one for spliced transcripts and one for unspliced transcripts—for each cell. This separation is the cornerstone for downstream applications such as RNA velocity analysis, which uses the relative abundance of unspliced (nascent) and spliced (mature) mRNA to infer the future state or “direction” of cell differentiation.
> 
> In summary, scRNA‐seq differentiates spliced from unspliced RNA by leveraging gene annotations during the read mapping process—assigning reads based on whether they align to exonic regions (spliced) or retain intronic regions (unspliced). This differentiation allows researchers to quantify the dynamics of gene expression and to predict cellular trajectories, an approach central to the RNA velocity framework. 

- **Spatial Transcriptomics:**  
  Methods like 10x Visium, seqFISH, and HybISS retain the spatial context of cells, which is crucial for understanding how local microenvironments affect cell fate decisions. Despite their high resolution, many spatial techniques lack the ability to measure the kinetic components (unspliced mRNA) needed for velocity estimation.

- **Data Integration and Domain Adaptation:**  
  Previous integration methods (e.g., SpaGE) have shown that spatial gene expression profiles can be enriched by leveraging reference scRNA-seq data to improve missing information. This integration is essential when combining data from different modalities and resolutions.

---

## 4. Relevant Theories

Several theoretical underpinnings support this work:

- **Differentiation and Trajectory Inference:**  
  The idea that cellular differentiation follows a trajectory—a continuum of state changes—is central to modern biology. The RNA velocity concept quantifies the rate and direction of these transitions.

- **Kinetic Modeling of Gene Expression:**  
  The theory behind RNA velocity rests on the kinetics of RNA processing. By measuring the balance between nascent (unspliced) and mature (spliced) transcripts, researchers can infer whether cells are in the process of "moving" from one state to another.

- **Machine Learning for Data Integration:**  
  Methods such as principal component analysis (PCA), k-nearest neighbors (kNN) regression, and domain adaptation (as implemented in the PRECISE method) enable the alignment and enrichment of spatial transcriptomics data with corresponding scRNA-seq datasets. These approaches allow predictions of unobserved features (e.g., kinetic mRNA states) and the transfer of metadata such as cell-type labels.

- **Graph-Based Clustering and Dimensionality Reduction:**  
  Techniques like UMAP and Leiden clustering help in visualizing high-dimensional data and identifying distinct cell states or regions within the tissue—critical steps for mapping out spatial differentiation trajectories.

---

## 5. Methods

The paper introduces **SIRV** (Spatial Inferred RNA Velocity), a multi-step pipeline that consists of four primary components:

1. **Integration:**
   - The spatial transcriptomics data (which only measures total mRNA) and the scRNA-seq data (which contains separate spliced and unspliced counts) are integrated using a domain adaptation method (based on PRECISE).
   - Shared genes between the two datasets are used to construct a common latent space (via PCA and the generation of principal vectors) so that the datasets are aligned

2. **Prediction of Spliced and Unspliced Expression:**
   - Using the aligned spatial and scRNA-seq data, SIRV employs kNN regression to predict the spliced and unspliced mRNA counts for each gene in the spatial dataset.
   - These predictions effectively “enrich” the spatial dataset with the kinetic information necessary for RNA velocity analysis.

> [!info]- KNN Regression
> **kNN Regression: An Overview**
> 
> k-Nearest Neighbors (kNN) regression is a non-parametric, instance-based learning method used for predicting continuous values. Instead of learning an explicit function from the training data, kNN regression makes predictions based on the values of the k most similar data points (neighbors) to a given query point. The similarity is typically defined by a distance metric (e.g., Euclidean or cosine distance). In its most common form, the predicted value is computed as an average (or weighted average) of the target values of these k-nearest neighbors. When using a weighting scheme, points that are closer to the query point receive higher weights, making their contributions more influential than those farther away.
> 
> **How kNN Regression Is Used to Predict Spliced and Unspliced Expression**
> 
> In this study, the authors aim to enrich spatial transcriptomics data—which usually captures only total mRNA—with kinetic information about splicing (i.e., levels of spliced and unspliced mRNA) that is available in a matching single-cell RNA sequencing (scRNA-seq) dataset. The steps are as follows:
> 
> 1. **Dataset Integration:**  
>    The spatial transcriptomics data and the scRNA-seq data are first integrated into a common latent space using domain adaptation techniques (e.g., via a method like PRECISE). This alignment ensures that each spatial cell has a corresponding representation in the scRNA-seq space, where splicing information is available.
> 
> 2. **Identifying Nearest Neighbors:**  
>    For each spatial cell $i$ in the integrated latent space, the algorithm identifies the k-nearest neighbors from the scRNA-seq data based on a chosen distance metric (in this study, cosine distance is used). These neighbors are the cells in the scRNA-seq dataset that have expression profiles most similar to those of the spatial cell.
> 
> 3. **Computing Weights:**  
>    A weight is assigned to each neighbor inversely proportional to the distance from the spatial cell.  
>    Mathematically, if $d(i, j)$ is the distance between the spatial cell $i$ and a scRNA-seq cell $j$ (which is one of the k-nearest neighbors), the weight $w_{ij}$ can be computed as:  
>    $$
>    \begin{eqnarray*}{w_{ij}} = 1 - {\rm{\;}}\frac{{{\rm{dist\;}}\left( {i,j} \right)}}{{\mathop \sum \nolimits_{j{\rm{\;}} \in NN\left( i \right)} {\rm{dist}}\left( {i,j} \right)}}\end{eqnarray*}
>    $$
>    The weight is then normalized to ensure that the weights for each spatial cell sum to 1.
> 
> 4. **Predicting Expression Values:**  
>    For each gene $g$ measured in the spatial dataset, the predicted expression values for spliced ($S'_{ig}$) and unspliced ($U'_{ig}$) transcripts in spatial cell $i$ are computed as weighted averages of the corresponding values from its k-nearest scRNA-seq neighbors:
>    $$
>    S'_{ig} = \sum_{j \in \text{NN}(i)} w_{ij} \times \text{SR}_{jg}
>    $$
>    $$
>    U'_{ig} = \sum_{j \in \text{NN}(i)} w_{ij} \times \text{UR}_{jg}
>    $$
>    where $\text{SR}_{jg}$ and $\text{UR}_{jg}$ are the spliced and unspliced expression values for gene $g$ in scRNA-seq cell $j$, respectively.
> 
> 
> **Why This Approach Is Effective**
> 
> - **Preserving Local Similarity:**  
>   By using the k-nearest neighbors in an aligned latent space, the method assumes that nearby cells in this space share similar transcriptomic and kinetic properties. This is a reasonable assumption since cells that are similar in overall gene expression are also likely to have similar splicing dynamics.
> 
> - **Weighted Averaging:**  
>   Weighting the neighbors by their similarity (with closer neighbors contributing more) helps ensure that the predicted spliced and unspliced expression levels for a spatial cell are biologically meaningful and reflect the local structure of the data.
> 
> - **Imputation of Missing Information:**  
>   Spatial transcriptomics technologies often do not capture the kinetic detail (i.e., separate spliced and unspliced counts) needed to compute RNA velocity. By transferring this kinetic information from a matched scRNA-seq dataset using kNN regression, the study enables spatial RNA velocity analysis, thereby opening a new window into observing differentiation trajectories in tissue contexts.
> 
> **In Summary**
> 
> - **kNN regression** is a method that predicts continuous values (here, spliced and unspliced expression) based on the weighted average of the target values from the k-nearest neighbors.
> - In this study, the spatial transcriptomics data is integrated with scRNA-seq data containing the kinetic (splicing) information.
> - For each spatial cell, the algorithm finds the k most similar cells in the scRNA-seq dataset and predicts its spliced and unspliced expression by taking a weighted average of those neighbors’ values.
> - This approach allows the authors to “impute” the missing splicing information in the spatial data, which is crucial for further analysis like RNA velocity, thereby enhancing the biological insights that can be drawn from spatial transcriptomics.
> 
> This clever use of kNN regression bridges the gap between data modalities and enriches spatial data with dynamic information derived from scRNA-seq, ultimately supporting a more nuanced understanding of cellular differentiation within tissues.

3. **Label Transfer:**
   - In addition to predicting kinetic measures, SIRV transfers metadata—such as cell-type labels and other annotations—from the scRNA-seq data to the spatial data using similar kNN-based regression methods.

4. **RNA Velocity Estimation:**
   - Once the spatial dataset is enriched with predicted spliced and unspliced expression values, the RNA velocity for each cell is calculated using established tools (e.g., scvelo).
   - The resulting velocity vectors are then projected onto the spatial coordinates to visualize cellular differentiation trajectories within their tissue context.

The authors applied SIRV to several datasets including developing mouse brain (using HybISS spatial data), mouse organogenesis (seqFISH), a developing chicken heart (10x Visium), and human osteosarcoma cells (MERFISH). Each application confirmed that spatial trajectory and differentiation patterns could be reliably inferred.

---

## 6. Results

Key results from using SIRV include:

- **Spatial Differentiation Trajectories:**  
  In the developing mouse brain, SIRV successfully reconstructed differentiation trajectories that aligned with known anatomical regions (e.g., midbrain-hindbrain boundaries, cortical hem, and dorsal diencephalon). The spatial RNA velocity vectors showed distinct branching corresponding to different developmental fates.

- **Reproducibility Across Datasets:**  
  SIRV was further validated on mouse organogenesis data and in datasets from the developing chicken heart and human osteosarcoma, demonstrating its robustness and general applicability across species and measurement technologies.

- **High Confidence and Robustness:**  
  The derived RNA velocity vectors exhibited high confidence scores. The authors also performed sensitivity analyses with varying hyperparameters (e.g., number of principal vectors and nearest neighbors), which showed that the inferred trajectories remained largely stable.

- **Metadata Integration:**  
  The successful transfer of cell identity and regional annotations from scRNA-seq to spatial data confirmed that the integration strategy was effective and could add biological interpretability to the spatial analysis.

---

## 7. Validations

The authors validated their approach through several means:

- **Comparison With Measured Data:**  
  They compared RNA velocity vectors derived from SIRV to those obtained directly from spatial datasets that do include kinetic information (like 10x Visium) or through other spatial methods (e.g., MERFISH). Consistency between predicted and measured velocities supported their method.

- **Cross-Dataset Consistency:**  
  The robustness of the SIRV pipeline was tested across multiple datasets from different tissues and developmental stages, strengthening the claim that its results were reliable and biologically relevant.

- **Hyperparameter Sensitivity Analysis:**  
  They systematically varied key model parameters (such as the number of principal vectors and the kNN regression settings) and observed that the overall spatial trajectories remained resilient to these changes, which adds confidence to the technique’s stability.

- **Statistical and Visualization Metrics:**  
  The authors employed metrics (e.g., weighted similarity scores) and visual confirmation (via UMAPs and overlaying velocity streamlines on spatial maps) as further evidence that the inferred trajectories were both statistically and biologically robust.

---

## 8. Implications

The development of SIRV has several broad implications:

- **Enhanced Understanding of Tissue Development:**  
  By enabling the inference of cellular differentiation dynamics in situ, SIRV allows researchers to study how cell fate decisions occur within the spatial context of tissue architecture—a dimension that is lost in dissociated scRNA-seq analyses.

- **Bridging Modalities:**  
  The method provides a blueprint for integrating high-resolution spatial transcriptomics data with more complete scRNA-seq datasets to "fill in the gaps" (i.e., the kinetic information), thus enriching spatial studies with dynamic insights.

- **New Analytical Opportunities:**  
  With spatial RNA velocities, one can potentially map out microenvironment-related influences on differentiation, track developmental boundaries, or assess the regional responses to perturbations in disease models.

---

## 9. Clinical Problem and Potential Applications

Although the primary focus of the paper is developmental biology, the innovations introduced by SIRV have significant clinical potential:

- **Cancer and Tumor Microenvironments:**  
  In oncology, understanding tumor heterogeneity and the dynamics of cellular states within a tumor mass is critical. Methods like SIRV could be used to map differentiation trajectories within cancer cells, revealing how certain cell populations may evolve drug resistance or contribute to metastasis.

- **Regenerative Medicine:**  
  Understanding the spatial dynamics of tissue differentiation and regeneration can inform tissue engineering strategies and improve regenerative therapies by identifying key differentiation cues that are controlled by local environments.

- **Precision Diagnostics:**  
  The ability to integrate spatial context with dynamic cell state information could lead to better biomarkers that consider not just cell type but also the regional behavior of cells within tissues, which is particularly important in complex diseases such as neurodegenerative disorders.

---

In summary, the paper presents a novel, integrative approach—SIRV—to enrich spatial transcriptomics data via scRNA-seq, thereby enabling the inference of RNA velocities with spatial resolution. This method pushes forward our ability to study how cells differentiate in tissue, offering new insights that can ultimately influence clinical strategies in cancer, regenerative medicine, and beyond. 
