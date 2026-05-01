# Scaling Optical Pooled Screens for Functional Genomics

**Speaker:** Noorsher Ahmed, PhD  
**Affiliation:** Postdoctoral Researcher, Lundberg Lab, Stanford University  
**Event:** State of Multi-omics and NGS 2026 Summit (GEN / Illumina)  
**Funding:** NIH, Stanford HAI, Anthropic  

---

## Background

A major ambition in modern biology is to build **virtual cells** — AI models capable of simulating, *in silico*, the effects of any genetic perturbation or drug treatment on cell state across multiple molecular readouts and biological scales. Achieving this requires extensive **perturbational data**: measurements of how cells respond when specific genes are disrupted, specific proteins are targeted, or environmental conditions are changed.

Two major paradigms currently generate perturbational data:

**Perturb-seq (genetic perturbation + transcriptomic readout):** A lentiviral library delivers CRISPR guide RNAs to knock out genes of interest; cells are then dissociated and profiled by single-cell RNA sequencing, yielding a perturbation-by-gene-expression matrix. This approach is highly scalable — whole-genome CRISPR screens are now routine — but expensive at the sequencing step, and the transcriptome does not always faithfully reflect protein-level and morphological changes that underlie disease phenotypes.

**Cell Painting / high-content imaging (drug perturbation + morphological readout):** Cells are treated with drugs or compounds and imaged after fluorescent staining. Morphological features (shape, texture, organelle organization) serve as readout. Scalable and inexpensive to run, but perturbations must be *arrayed* (one compound per well), preventing the combinatorial depth achievable with pooled genetic screens.

**Optical Pooled CRISPR Screening (OPS)** combines the strengths of both. Cells receive a pooled lentiviral CRISPR library (scalable, whole-genome capable), and identity is recovered not by sequencing but by **in situ sequencing of guide RNA barcodes** imaged directly on the plate. Phenotype is measured by high-content imaging — morphology, protein localization, live-cell dynamics — at a cost that is orders of magnitude lower than single-cell sequencing. OPS is particularly well-suited for diseases with known imaging phenotypes (protein aggregation, subcellular mislocalisation, specific morphological hallmarks), many of which are invisible to transcriptomic readouts.

A key enabling resource for this work is the **Human Protein Atlas** — a public database mapping the subcellular localisation of the human proteome using immunofluorescence microscopy, with >25,000 antibodies and >2 million annual users. More than **14,000 proteins** have been localized to 35 cellular structures and 14 organelle proteomes. Critically, ~60% of proteins show pleiotropic localization (multiple compartments), and 21% display spatiotemporal dynamics — meaning the baseline proteome is not static but context-dependent. This resource serves as both a reference and a training dataset for the vision AI models used in Ahmed's work.

---

## Section 1: The Case for Optical Pooled Screening

Ahmed framed the challenge of perturbation biology as inherently multimodal: cells transition through a high-dimensional manifold of possible states in response to perturbations, and both the perturbation space (genetic, chemical, environmental) and the readout space (transcriptomic, proteomic, morphological, temporal) are vast and incompletely sampled by any single assay.

He made a direct argument that transcriptomics is insufficient for many biologically and pharmaceutically important phenotypes. Drawing on his PhD work in RNA biology (Gene Yeo lab), he noted that diseases like neurodegeneration involve **stress granule formation, protein mislocalisation, and translational changes** that are clearly visible by imaging but may produce no detectable RNA-level signal. Furthermore, the transcriptome-proteome correlation is weak, meaning perturbation-by-RNA-expression matrices may be measuring a layer of biology removed from actual cellular function. In practice, he noted, even with single-cell resolution in Perturb-seq, researchers routinely resort to **pseudo-bulking** (averaging across cells) to achieve statistical power, which partly defeats the purpose of single-cell resolution.

OPS was framed as the natural complement to Perturb-seq: used best after a transcriptomic screen has identified candidate targets or biological hypotheses, OPS then enables scalable phenotypic validation against morphological disease hallmarks already known to the field.

---

## Section 2: The DECODE Robot — Automating the Wet Lab

The primary bottleneck in early OPS implementations was the wet lab. A whole-genome OPS screen requires transducing millions of cells with a pooled viral library, expanding them, seeding plates, staining, imaging multiple modalities, performing in situ sequencing, and repeating across many plates — a multi-week, error-prone manual process.

Ahmed and colleagues built the **DECODE Robot**, a three-component automated system:
- A **liquid handler** performing all pipetting chemistry
- A **microscope** (built by Cephla) for automated multi-modal imaging
- A **robotic arm** coordinating plate movement and scheduling

The system executes an asynchronous, **DAS (Dynamic Asynchronous Scheduling)** pipeline that parallelizes steps across wells and plates, reducing a process that would take a human weeks to under **24 hours for a whole-genome screen**.

On cost efficiency, Ahmed presented simulated estimates (not benchmarked figures) suggesting that at billion-cell scale, OPS with robotics can remain well under $1 million per experiment — orders of magnitude cheaper than sequencing-based approaches at equivalent cell numbers.

The multi-modal imaging challenge presents an additional computational problem: OPS experiments combine data from multiple microscope types (live-cell imaging on a Leica, fixed spatial proteomics on a spinning-disc confocal, in situ sequencing on an epifluorescent scope). These instruments produce images at different pixel sizes, magnifications, tile sizes, and optical qualities that must be computationally registered and reconciled.

---

## Section 3: High-Performance Computer Vision for Image Analysis

To handle the multi-terabyte image data generated by whole-genome OPS, Ahmed's team built a GPU-accelerated, fully parallelised image analysis pipeline using Stanford's Slurm HPC clusters:

- Images are stitched into **OME-ZARR pyramidal streaming format** (compatible with tools like OME-NGFF), enabling rapid access and efficient cell segmentation
- **Cell segmentation** is performed per well, per field of view, per plate simultaneously
- **In situ sequencing base-calling** assigns guide RNA barcodes to individual segmented cells
- **Foundation model embeddings** (from vision transformers trained on HPA data) extract per-cell phenotypic features
- Downstream analysis is packaged into the **AnnData format** familiar to single-cell biologists, enabling integration with tools like NVIDIA RAPIDS single-cell for GPU-accelerated analysis

Full analysis of three- to five-plate whole-genome screens completes within a day of compute time.

The need for automated, unsupervised featurization was addressed by the **Subcell foundation model** — a vision transformer trained on the entirety of the Human Protein Atlas data by colleagues in the Lundberg lab (led by Ankit, Zoe, and Konstantin). Subcell:
- Outperforms or matches prior state-of-the-art on downstream tasks including predicting protein-protein interactions (from STRING database) and pathway membership (Reactome)
- Shows interpretable attention heads corresponding to specific subcellular compartments, indicating that the model has learned genuine cellular morphology
- Produces embeddings that cleanly separate **cell line identity** from **protein localisation** in orthogonal dimensions — enabling cross-cell-line comparison of screen hits without confounding by cell-type morphology

This resolves a long-standing challenge: OPS experiments performed in different cell lines (e.g., HeLa vs. HEK293) or at different time points can now be compared in a shared embedding space.

---

## Section 4: Agentic Screen Design — Scaling Intelligence, Not Just Data

Ahmed raised a deeper mathematical problem articulated by Aviv Regev and Brian Cleary: if perturbation biology aims to map **combinatorial gene-gene and gene-drug interactions** — the actual mode of biological regulation — the number of experiments required grows exponentially and exceeds the total number of cells on earth at whole-genome scale. Whole-genome screens, despite their power, represent a brute-force approach to a fundamentally combinatorial problem.

His proposed solution is **agentic perturbation screen design**: instead of running a whole-genome screen every time, use an AI agent to intelligently select the minimal set of perturbations most likely to test a given biological hypothesis, effectively compressing the experimental space. This work is supported by **Anthropic** and built on advances in **graph-based retrieval-augmented generation (graph RAG)** with specialist sub-agents, enabling the system to traverse biological knowledge graphs to derive experimentally tractable perturbation sets.

Ahmed positioned this as a log-N rather than exponential scaling approach: intelligent hypothesis-driven design that reduces the number of experiments needed while maintaining inferential power.

---

## Q&A Highlights

**Q: Where do optical pooled screens best outperform transcriptomic methods?**  
When diseases have known imaging hallmarks — protein aggregation, mislocalisation, morphological changes — OPS captures the relevant phenotype directly and cheaply. OPS is less suited to exploratory "fishing expeditions" where the phenotype is unknown and transcriptomics provides the broadest initial sweep. The two approaches are **complementary**: Perturb-seq is ideal first-in, OPS for scaling up once targets or morphological hallmarks are identified.

**Q: How sensitive is OPS to the choice of cell model?**  
Sensitivity is comparable to any high-content imaging screen. Engineered workhorse cell lines that work for high-content imaging will work for OPS as long as Cas9 machinery can be introduced. The **NIS-seq, Perturb-View, and Zombie** protocols have substantially improved guide RNA expression and in situ sequencing fidelity across diverse cell types, including non-cancer cell lines. Extension to organoids and in vivo tissue is the current frontier, with proof-of-concept demonstrations in those systems already published.

**Q: What is the current bottleneck for scaling to billions of cells?**  
Bottlenecks have shifted as solutions are found: wet lab (addressed by robotics), computation (addressed by GPU pipelines), and now **cell culture at scale** — keeping enough cells alive and healthy to feed the imaging pipeline. As each bottleneck is solved, the next one emerges, which Ahmed viewed optimistically as a sign of healthy technological progress.

**Q: What is the biggest remaining challenge?**  
The **mathematical limit** of combinatorial perturbation space. Even if individual screens become fast and cheap, the combinatorial space of gene-gene and gene-drug interactions is fundamentally intractable by exhaustive enumeration. Compression strategies and intelligent experimental design (agentic screen planning) are likely necessary solutions within the five-year horizon.

---

## Summary

Noorsher Ahmed presented a vision for scaling Optical Pooled CRISPR Screening into a high-throughput, affordable, and automated platform for phenotype-driven perturbation biology. The work addresses three pillars: (1) robotic automation of wet lab chemistry (DECODE Robot, whole-genome screens in <24h); (2) GPU-accelerated computer vision pipelines that process multi-terabyte, multi-instrument imaging data within a day; and (3) AI-assisted screen design to navigate combinatorial perturbation space more intelligently than brute-force whole-genome approaches. The Subcell foundation model, trained on the Human Protein Atlas, enables unsupervised phenotyping across experiments and cell lines by learning genuine subcellular morphology. Ahmed's broader intellectual contribution is to reframe perturbation biology as requiring not just more data but smarter, more targeted data — a theme that resonates throughout the broader summit discussion. The computational challenges are now arguably more constraining than the biological or technical ones, and the mathematical limits of combinatorial perturbation space represent the field's next fundamental frontier.
