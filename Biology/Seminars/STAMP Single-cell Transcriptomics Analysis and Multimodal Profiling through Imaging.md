# STAMP: Single-cell Transcriptomics Analysis and Multimodal Profiling through Imaging

#paper #candida 

---

## Motivation and Research Question

Many single-cell RNA sequencing (scRNA-seq) methods are costly, low-throughput, and destroy cell morphology. The authors ask:  
How can we profile millions of single cells—capturing RNA, protein, and structure—at scale, cost-efficiently, and without sequencing?

---

## Background

- Single-cell sequencing revolutionized cell atlases but remains limited by droplet inefficiencies, high costs, and loss of spatial context.  
- Imaging-based spatial transcriptomics and proteomics have expanded gene panels but have been confined to tissue sections.  
- STAMP repurposes these platforms for **cells in suspension**, enabling massive single-cell profiling while retaining morphology.

---

## Data Types & Acquisition Methods

- **Sample types**: Cell lines, PBMCs, stem cells, FFPE tissue nuclei.  
- **Modalities**:  
  - RNA transcripts via fluorescent oligo probes (FISH-style barcodes + cyclic imaging)  
  - Proteins via DNA-barcoded antibodies  
  - Morphology via H&E and IF markers (DAPI, PanCK, CD298)  
- **Platforms**: Xenium Analyzer, CosMx SMI, MERSCOPE, PhenoCycler Fusion  
	- requires specific instruments

---

## Theoretical Framework

- **Combinatorial barcoding**: Each target is assigned a unique on–off fluorescent pattern across imaging cycles, enabling thousands of targets with few colors.  
- **Single-molecule sensitivity**: High-NA optics detect individual transcripts or antibody-DNA spots.  
- **Spatial retention**: Cells remain in their stamped positions, preserving morphology for joint analysis.

---

## Methodology

### STAMP Workflow

1. **Fixation & Permeabilization**  
2. **Stamping**  
   - Cells in suspension are “printed” onto glass slides in defined arrays (sub-STAMPs).  
3. **Probe Hybridization**  
   - RNA targets: gene-specific oligo probe panels (1K–6K genes)  
   - Proteins: oligo-conjugated antibodies  
4. **Cyclic Imaging & Decoding**  
   - Multiple rounds of fluorescence imaging; probes are stripped or quenched between cycles  
5. **Image Processing**  
   - Cell segmentation (DAPI + membrane markers)  
   - Spot detection, barcode decoding, and feature extraction  
6. **Analysis**  
   - Clustering (InSituType), UMAP/PCA, pathway scoring (AUCell), differential expression, cell-cell communication (CellChat)

### Platform & Panel Summary

| Platform      | Panel                               | Targets        | Max Cells/Slide    |
|---------------|-------------------------------------|----------------|--------------------|
| Xenium        | Prime 5K Human Pan Tissue & Pathways| ~5,000 genes   | Millions           |
| CosMx SMI     | Human 6K Discovery                  | ~6,000 genes   | Millions           |
| MERSCOPE      | PanNeuro Cell Type (500 genes)      | 500 genes      | Hundreds of thousands |
| PhenoCycler   | Custom RNA + IF markers             | Variable       | Multi-sample arrays|

---

## Key Results

### 1. Sequencing-free Single-cell Genomics (Fig. 1)
- Mixed LNCaP, MCF-7, SK-BR-3 cancer cells (~35K each) in sub-STAMPs.  
- Achieved ~3,600 transcripts & 413 genes per cell; clear UMAP clusters by cell line.  
- Retained morphology via post-STAMP H&E and IF overlays.

### 2. Ultra-low Input Sensitivity (Fig. 2)
- Sub-STAMPs with as few as 100 cells: ~85% recovery.  
- Gene counts plateau above 250 cells; nuclear vs whole-cell profiling highly correlated.

### 3. Cross-Platform Multiplexing (Fig. 3)
- 27 samples stamped across Xenium and CosMx slides.  
- High Pearson correlations of counts, features, and cell area across replicates and platforms (>0.9).  
- Harmony integration removed batch effects; LISI scores confirmed integration quality.  
- Pathway enrichment (e.g., lymphocyte, glycolysis/hypoxia) consistent across assays.

### 4. Immuno-phenotyping PBMCs (Fig. 4)
- Stamped ~1.7 M PBMCs with a 380-gene Immuno-Oncology panel.  
- Identified 13 major immune clusters (T, B, myeloid), then 31 refined cell states (8 CD4+ subsets, 8 CD8+ subsets, NK progenitors).  
- Comparable sensitivity to 10× scRNA-seq on overlapping genes; superior marker detection efficiency.

### 5. Perturbation Studies
- PBMCs stimulated with LPS or anti-CD3/CD28 for 4 h and 24 h.  
- Changes in T cell subsets and monocyte activation validated via volcano plots and CellChat-inferred ligand–receptor networks.

---

## Key Figures & Tables

| Figure/Table       | Description                                                     |
|--------------------|-----------------------------------------------------------------|
| Fig. 1             | Imaging workflow, QC metrics, UMAP clusters, H&E + IF overlays |
| Fig. 2             | Recovery & QC at low cell counts; cell vs nucleus comparison    |
| Fig. 3             | Multiplex layout, replicate correlations, PCA integration, pathway scores |
| Fig. 4             | PBMC cluster UMAPs, marker dot plots, stimulation response plots, CellChat networks |
| Table S1           | Sample IDs, cell types, culture conditions per sub-STAMP        |
| Table S2           | Probe panel gene lists                                          |

---

## Validation Strategies

- **Technical replicates** across slides/platforms (high correlation of counts, genes, areas).  
- **Benchmarking against scRNA-seq** reference (Spearman correlation of gene signatures; sensitivity comparisons).  
- **Clustering validation**: marker gene heatmaps, correlation with known cell line signatures.  
- **Perturbation coherence**: expected shifts in immune subsets and gene expression under LPS/CD3 stimuli.  

---

## Implications & Clinical Applications

- **Scalable profiling**: millions of cells per slide, multimodal in a single run—ideal for cell atlasing, drug screens, and large-cohort studies.  
- **Cost reduction**: eliminates sequencing reagents and library prep, lowering per-cell costs at high throughput.  
- **Spatial context retention**: combines molecular profiles with morphology—critical for pathology and tumor microenvironment studies.  
- **Clinical utility**: high-resolution immune monitoring (e.g., cancer immunotherapy), rare circulating cell detection (e.g., CTCs), and large-scale diagnostic assays without sequencing infrastructure.

STAMP bridges the gap between high-content imaging and single-cell genomics, offering a versatile, affordable platform for both basic research and clinical translation.