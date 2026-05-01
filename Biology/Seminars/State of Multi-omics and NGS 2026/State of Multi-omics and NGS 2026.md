# State of Multi-omics and NGS 2026

Summit hosted by GEN and sponsored by Illumina

## Keynote: Spatial Multiomics Reveals 3D Alzheimer’s Hippocampal Pathology

Miranda Orr, PhD, Associate Professor of Neurology at Washington University School of Medicine
Data from Bruker Spatial Biology platform


## Scaling Optical Pooled Screens for Functional Genomics

Noorsher Ahmed, PhD, Stanford University
[Subcell: a proteome aware vision foundational model](https://pubmed.ncbi.nlm.nih.gov/41278937/)
## Multiomics Data Management

Chris Dwan, Data Management for Multiomics

Two quotes from Nevin Young, Donald Knuth

## Blueprints for Breakthroughs: Creating a Multiomic Future of Biological Discoveries and Medical Advances (Sponsored by Illumina)

Bodour Salhia, PhD, Department Chair at Keck School of Medicine, USC
Eric Green, MD, PhD, Chief Medical Officer at Illumina

## NGS Hot Goss: A Review of NGS News from the Bloggers

Keith Robison, PhD, Automation Visioneer at Ginkgo Bioworks
Shawn Baker, PhD, Genomics Consultant at SanDiegOmics



## Single Cell Genomics

Holger Heyn, PhD, ICREA Professor at Centro Nacional de Análisis Genómico (CNAG), Barcelona

Here's a tightened version:

---

**Pixel and Object-Level Cell Type Classifier**

Developed two napari plugins for pixel- and object-level classification of microscopy images, producing structured annotations for downstream scene graph generation.

- **Pixel-Level Classification:** Extended an existing napari plugin with advanced feature channels — Hessian determinant, difference-of-Gaussians shape index, and local binary patterns — alongside standard intensity, texture, and edge features to improve foreground/background discrimination.

- **Object-Level Classification:** Built an end-to-end pipeline that segments foreground pixels into candidate objects, applies K-Means + SVM on log-transformed pixel areas to filter true objects from noise, extracts per-object morphological and intensity features, performs dimensionality reduction via PLS-DA, and trains an XGBoost classifier to assign cell/nuclei types.

- **Performance Optimization:** Optimized feature caching, incremental retraining (reusing cached features for previously processed slices), and model I/O to minimize redundant computation across iterative label–train–predict cycles on 3D Z-stacks.

---

Changes made:
- Replaced passive constructions with active verbs
- Removed "including" lists where the structure already implies them
- Merged redundant phrases ("cell/nuclei types" kept once, not twice)
- Made the optimization bullet concrete (incremental retraining, not just "caching")
- Cut filler ("allowing classification to be performed") in favor of direct claims