# Spatial Multiomics Reveals 3D Alzheimer's Hippocampal Pathology

**Speaker:** Miranda Orr, PhD  
**Affiliation:** Associate Professor of Neurology, Washington University School of Medicine; Co-Director, Tracy Family SILC Center; Research Health Scientist, St. Louis VA  
**Event:** State of Multi-omics and NGS 2026 Summit (GEN / Illumina)  
**Disclosure:** Orr's lab is a designated Spatial Biology Center of Excellence by Bruker; all data were generated on Bruker Spatial Biology instruments.

---

## Background

Alzheimer's disease (AD) is the leading cause of dementia and the most feared condition of aging, surpassing fear of heart attack, stroke, or cancer. The disease is defined for research purposes by the **ATN framework** (updated by NIA/Alzheimer's Association), which captures three core pathological dimensions:

- **A (Amyloid-β):** Extracellular plaques formed by aggregated amyloid-β protein.
- **T (Tau):** Intracellular **neurofibrillary tangles** (NFTs) formed by hyperphosphorylated tau, a microtubule-associated protein. NFTs are among the most common intraneuronal pathologies across all neurodegenerative diseases.
- **N (Neurodegeneration):** Widespread neuronal loss and tissue atrophy.

An expanded framework now also includes **ISB**: inflammation, synaptic dysfunction, and vascular contributions — reflecting that AD is a multifactorial, multi-cell-type disease whose pathology is detected primarily at the level of proteins and post-translational modifications.

**Cellular senescence** is a stress-response program relevant to this work. Damaged cells that can neither repair nor die via apoptosis enter senescence: they undergo dramatic morphological, transcriptomic, proteomic, and metabolomic changes. They upregulate both pro-apoptotic and pro-survival pathways, becoming trapped in a damaged-but-alive state. Their hallmark is the **senescence-associated secretory phenotype (SASP)** — secretion of pro-inflammatory cytokines, chemokines, and extracellular matrix remodeling enzymes that attract immune cells and can transform neighboring cells into a senescent state. Because they resist normal clearance, senescent cells have been called "toxic zombie cells."

**Spatial multiomics** combines spatially resolved measurements of RNA (whole transcriptome) and protein (multiplexed antibody panels) within intact tissue sections, preserving the cellular and tissue architecture that is lost in single-cell dissociation experiments. The Bruker **COSMIC Spatial Molecular Imager** can simultaneously profile >18,000 transcripts and >72 proteins across >85,000 cells in a single section, resolving both location and identity at single-cell resolution.

---

## Section 1: Tau Tangles and Cellular Senescence — The Central Hypothesis

Orr's lab focuses on understanding why **neurons with neurofibrillary tangles survive despite being among the sickest cells in the brain**. These neurons appear almost "strangled" by tau aggregates but persist for an estimated 20+ years. Paradoxically, although tangle burden correlates strongly with disease severity, neuronal loss exceeds tangle counts by orders of magnitude — dozens or hundreds of neurons die for every visible tangle. This apparent contradiction mirrors the biology of cellular senescence: cells that survive in a damaged, toxic state rather than dying cleanly.

Building on this, the lab hypothesized that **neurons with tangles have entered the senescent state**, and that this explains both their persistence and their contribution to disease pathogenesis. Testing this hypothesis has required overcoming a fundamental challenge: senescent cells are notoriously difficult to identify because their definition requires simultaneous measurement of multiple molecular and morphological features rather than any single marker.

---

## Section 2: Computational Evidence for Neuronal Senescence

The lab's first approach used **microarray data from laser-capture microdissected (LCM) neurons** sorted from postmortem AD brains — with and without visible tangles. Transcriptomic analysis revealed that neurons with tangles expressed a gene expression signature consistent with cellular senescence.

Subsequently, the team applied an **eigengene approach** to published single-nucleus RNA sequencing (snRNA-seq) datasets from AD brains. Eigengenes summarize the coordinated expression of an entire gene pathway as a single continuous score, enabling pathway-level analysis at single-cell resolution. This unbiased screen found that approximately **2% of brain cells in AD are senescent**, and of those, **>95% are excitatory neurons** overlapping with tangle-bearing neuron signatures.

While these computational results were publishable and field-advancing, they remained indirect — predictions from transcriptomic profiles rather than direct observations. The lab's next ambition was to **validate these predictions spatially** using the coordinates of individual cells within brain tissue.

---

## Section 3: Spatial Validation Attempt — Where More Data Was Needed

To test whether the eigengene-predicted tangle signature could correctly identify tangle-bearing neurons within spatial transcriptomics data, the lab ran a ground-truth experiment on **postmortem hippocampal tissue** (mid-Braak stage Alzheimer's disease) profiled on the COSMIC spatial molecular imager at whole-transcriptome resolution.

Eigengenes were derived from two independent datasets:
1. LCM-dissected neurons (entorhinal cortex, mid-Braak stage)
2. FACS-sorted neurons stained for phospho-tau AT8 (dorsolateral prefrontal cortex, advanced AD)

A scientist manually identified **239 ground-truth tangles** from the AT8-stained tissue. The data scientist then used the eigengene models to computationally predict which cells had tangles, without seeing the scientist's selections. Results were visualized using color overlays: green (computationally predicted), yellow (scientist-selected), and purple (overlap).

**Results:** The LCM-derived eigengene predicted **1,132 cells as tangles**, with only **70 overlapping** with the 239 ground-truth tangles. The FACS-derived eigengene predicted **1,119 tangles** with **84 overlapping**. The prediction was poor — far more false positives than true positives, and low sensitivity.

Rather than treating this as a failure, the team reframed it as a question: what does "more data" mean? They identified five dimensions along which data quality or completeness could be expanded:

| Dimension | Before | After |
|---|---|---|
| Cells per slide | 96 | 85,000+ |
| Transcripts profiled | 1,000 | 18,934 |
| Number of brains | 20 | 180+ |
| Brain regions per case | 1 | Multiple |
| Proteins profiled | 87 | 1,200+ |
| Serial sections per case | 1 | 8 |

---

## Section 4: More Proteins Enable Pathway-Level Spatial Analysis

The lab used the **GeoMx Digital Spatial Profiler** to precisely select neurons with or without tangles (identified by AT8 phospho-tau staining and MAP2/HUD neuronal markers) and profile them for a multiplexed protein panel. When expanding from **87 proteins** to **>1,200 proteins**, the data shifted from differential expression of individual proteins to **differential pathway enrichment** — and the enriched pathways in tangle-bearing neurons pointed strongly to cellular senescence signatures. This was the first direct, non-computational evidence linking tangle neurons to a senescent proteomic state.

Key insight: "We're no longer guessing about the biology, but actually seeing it." More proteins allowed the team to make biologically interpretable conclusions without needing to infer senescence from transcriptomic proxies.

---

## Section 5: 3D Reconstruction from Eight Serial Sections

The centerpiece of the talk was a novel experiment profiling **eight serial hippocampal sections (5 µm each)** from a single case on the COSMIC spatial molecular imager. Each section was profiled for:
- **72-plex protein panel** (including five phospho-tau variants, neuronal markers, astrocyte/microglial markers)
- **18,934-plex whole transcriptome RNA panel**

Tissue quality was high, field-of-view placement was consistent across all eight sections (250 fields of view per section), and 3D reconstruction was performed in collaboration with **Ariadne**.

### 3D Visualization of Hippocampal Pathology

The 3D reconstruction revealed stark spatial heterogeneity of pathology around the hippocampus:
- In the **dentate gyrus**: high density of healthy (yellow) neurons, few tangles
- Moving toward **CA1**: progressive replacement of healthy neurons by AT8+ phospho-tau signal (red), astrocyte (green), and microglial (purple) populations
- In **CA1 proper**: virtually complete loss of healthy neurons; the region is dominated by neuroinflammation and tangle-bearing cells

This spatial gradient was not previously appreciable from single 2D sections and illustrates how disease severity varies dramatically across hippocampal subfields.

### Transcript Counts: 2D vs. 3D

A key finding concerns how cell span across serial sections affects transcript quantification. Healthy neurons spanning 2–3 sections show relatively uniform MAPT (tau gene) transcript density per section. Neurons with tangles often **span more sections** (3–4), and critically, **transcripts are highly unevenly distributed** — concentrated in 1–2 sections and absent from others.

Quantitative comparison (mean transcripts per cell):

| Gene | 2D (single section) | 3D (all sections) | Increase |
|---|---|---|---|
| MAPT | 2.61 | 5.17 | ~2× |
| SNAP25 | 29.7 | 52.0 | ~1.75× |
| TMM591 | 4.25 | 8.05 | ~1.9× |
| Top 1,000 transcripts | 995 | 1,610 | ~60% |

**Implication:** Single-section analyses systematically undercount transcripts, especially in large, morphologically complex neurons. Cells with extensive dendritic and axonal projections have transcripts distributed across multiple sections; capturing the full complement requires 3D profiling.

### Why Senescent Cells May Be Particularly Affected

To illustrate the morphological transformation of senescent cells, Orr showed high-resolution 3D nuclear imaging from Bruker's **Paintscape platform** (419 chromosome probes via Chromopaint PanChromo assay). Healthy nuclei occupy a normal volume; cells induced into senescence can expand **tenfold** in nuclear volume. The serial-section data already hints at this phenotype: tangle-bearing (senescent) neurons span four sections while healthy neurons span only two.

### Protein Stability Across Serial Sections

In contrast to RNA, **protein expression is remarkably stable across serial sections**. Mean fluorescence intensity per cell for MAP2/HUD (neuronal marker) was 23.4 (2D) vs. 24.0 (3D) — essentially identical. Most phospho-tau variants (tau-199, tau-396) show flat, horizontal trajectories across the eight sections. One exception: the AT8 tangle marker shows steeper inter-section variability, similar to RNA, possibly reflecting genuine biology of tangle maturation and localization rather than technical noise.

This stability of protein across sections makes protein an ideal **anchor** for 3D reconstruction — defining cell boundaries that allow correct assignment of transcripts to their parent cells.

---

## Section 6: Responsible Data Generation

Orr concluded with a philosophical note that generated the most discussion. The rapid scaling of spatial multiomics raises a risk: labs are incentivized to generate enormous datasets because technology now makes it possible. Her argument is that **quantity does not substitute for fidelity**:

> "Just because we can doesn't mean we should."

She observed that the lab learned more about tau pathology from **87 proteins than from 18,000 transcripts**, and more from **8 brains with 1,200 proteins** than from **180 brains with 87 proteins**. This is a striking inversion of the "more samples = better science" assumption common in the field.

Her proposed path forward includes **ground-truth experiments** — for example, running spatial multiomics on neurosurgical biopsy tissue collected with minimal postmortem delay and comparing it to biorepository-fixed tissue, or performing controlled mock-postmortem interval studies in animal models. These unglamorous methods experiments are necessary to understand how postmortem interval, fixation protocol, and tissue processing affect RNA and protein signal fidelity before building AI models on these data.

---

## Q&A Highlights

**Q: What is the best way forward for the spatial biology field?**  
Orr advocated for ground-truth experiments: comparing freshly collected neurosurgical tissue profiled immediately on spatial platforms against standard biorepository tissue, and performing mock postmortem interval studies in animal models. She argued the field needs to understand data fidelity before AI models are trained at scale on potentially degraded or incomplete observations.

**Q: Do you see a future for LCM with mass spec, given your preference for proteins?**  
Yes. Spatial mass spec has an important place, particularly for unbiased protein discovery. However, mass spec detects high-abundance proteins preferentially and misses low-abundance targets. Antibody-based panels remain necessary for low-abundance proteins of interest. The ideal approach combines both.

**Q: How do you normalize expression across serial sections?**  
The team is still developing normalization strategies. Currently, transcripts per cell and mean fluorescence intensity per cell are used as primary metrics.

**Q: Why does protein add cell boundaries but RNA cannot?**  
RNA transcripts are simply imaged as point clouds. Without a structural marker (protein-based cell boundary), there is no way to determine which transcripts belong to which cell, especially in neurons with long processes where local translation and transcript transport carry RNA far from the cell body. Protein markers trace the full three-dimensional extent of the cell.

**Q: Is protein important across fields or specific to neuroscience?**  
Orr argued it is broadly applicable: "When we're getting to the nuts and bolts of what's really happening in that cell, it's happening at the protein level." RNA is important but is one step removed from actual cellular activity.

**Q: Can AI compound problems if trained on low-fidelity data?**  
Yes. Orr expressed concern that foundation models are now being built on existing data with an implicit assumption that those data faithfully reflect biology. If the data have systematic artifacts from postmortem tissue, fixation, or 2D truncation of 3D cells, those artifacts may be baked into the models. The field needs open dialogue and better data quality benchmarks before building at scale.

---

## Summary

Miranda Orr presented cutting-edge work from her lab on understanding neurons with neurofibrillary tangles in Alzheimer's disease through the lens of cellular senescence and spatial multiomics. Her central question — whether tangle-bearing neurons are senescent, and what that means for AD pathogenesis — has evolved from a purely computational hypothesis toward direct spatial validation, with clear steps both forward and back.

The key scientific advances reported include: (1) proteomic pathway analysis at >1,200 proteins showing direct senescence pathway enrichment in tangle neurons; (2) a 3D reconstruction of eight serial hippocampal sections revealing dramatic spatial gradients of pathology across hippocampal subfields; (3) the discovery that RNA is severely undercounted in 2D analysis (approximately 60% undercount for the top 1,000 transcripts) due to cell span across sections; and (4) evidence that protein is far more stable across serial sections than RNA, making it the preferred analyte for 3D cellular reconstruction in fixed postmortem tissue.

The talk's broader argument — that the field needs better data rather than simply more data, and that responsible generation of spatial multiomics data requires ground-truth fidelity experiments — is both timely and challenging to implement, particularly given the current momentum toward AI-scale data collection. Orr's work represents a model of iterative, hypothesis-driven spatial multiomics that prioritizes interpretability and biological validation over dataset size.
