# Multimodal and Multiscale Views on a Million Single Cells

**Speaker:** Holger Heyn, PhD  
**Affiliations:**  
- ICREA Professor, Centro Nacional de Análisis Genómico (CNAG), Barcelona, Spain  
- Chief Scientific Officer and Co-Founder, Omniscope  
- Co-Chair, Standards and Technology Working Group, Human Cell Atlas (HCA)  
- Co-Chair, HCA Spatial Program  

**Host:** Kevin Davis, GEN Editorial Director  
**Event:** State of Multi-omics and NGS 2026 Summit (GEN / Illumina)  
**Duration:** Approximately 50 minutes (ran over schedule)

---

## Background

**Single-cell genomics** refers to the molecular profiling of individual cells rather than bulk tissue preparations. This is critical because tissues are composed of heterogeneous cell populations — neurons, glia, immune cells, fibroblasts — each with distinct transcriptomes, epigenomes, and proteomes. Bulk measurements average across this heterogeneity and can miss rare cell types, intermediate states, and cell-type-specific responses. The key technologies include single-cell RNA sequencing (scRNA-seq), single-nucleus RNA sequencing (snRNA-seq for frozen or fixed tissue), CITE-seq (combined RNA and protein surface marker profiling), and spatial transcriptomics (which adds tissue localization).

**Spatial transcriptomics** measures gene expression in the context of tissue architecture — where a cell is located within a tissue section relative to other cells. Methods fall into two broad categories: (1) **imaging-based** (e.g., MERFISH, Xenium from 10x, CosMx from Bruker), which directly images individual RNA molecules within intact cells by fluorescence in situ hybridization; and (2) **sequencing-based** (e.g., Visium from 10x, Slide-seq), which spatially barcodes RNA molecules extracted from a tissue section and assigns them to grid positions by sequencing. Imaging-based methods achieve true single-cell resolution; sequencing-based methods achieve broad transcript coverage with spatial positioning.

**The Human Cell Atlas (HCA)** is an international consortium launched in 2016 to systematically map every cell type in the human body — across all tissues, developmental stages, and disease states — using single-cell technologies. By 2026 it encompasses ~4,000 members across 100 countries, has released >200 million cells across >30 atlases, and generated >450 publications cited more than 100,000 times.

**T-cell receptor (TCR) and B-cell receptor (BCR) repertoire sequencing** reads the unique, near-randomly generated receptor sequences that are present on individual T and B lymphocytes. Because each lymphocyte expresses a unique receptor sequence, and because antigen-specific lymphocytes expand clonally upon activation, tracking TCR/BCR clonotypes over time provides a high-resolution read of immune history, vaccine response, anti-tumor immunity, and autoimmune activity.

---

## Section 1: Human Cell Atlas 2.0 — Transition to Spatial, Disease, and Foundation Models

Heyn opened by placing the talk in the context of the HCA's transition from its first to its second phase. Version 1, spanning 2016–2026, used single-cell technologies to build **single-organ atlases of the healthy human body**. Thirteen of eighteen organ system atlases have been published; the remaining five will be published during 2026. The complete first-phase atlas represents >200 million cells across >30 atlases, assembled within a data ecosystem including analysis tools, metadata standards, and public portals.

**HCA 2.0** has four defining characteristics:

1. **Spatial resolution:** Moving from dissociated single-cell profiles to spatially resolved profiles. The single-cell first phase scattered cells from their tissue contexts; spatial genomics returns them to those contexts. Initially in 2D (section-level profiling, which is the commercial standard), with a roadmap toward 3D tissue and organ reconstruction.

2. **Disease context:** Expanding from healthy individuals alone to include disease states, enabling characterization of "natural perturbation" — the full plasticity space of cells in the context of pathology — and identification of druggable targets and disease mechanisms.

3. **Global representation:** Data from genetically diverse individuals across ethnicities and geographic regions, enabling multi-modal integration across different genetic backgrounds and more representative foundation models.

4. **Foundation models:** Building AI models trained on the complete, spatially resolved, multimodal, globally representative atlas — models that can represent full cellular plasticity across organ systems, health and disease states, and genetic backgrounds.

The organizational structure of HCA 2.0 consists of four tracks: (1) the 18 organ bio-networks providing samples and community infrastructure; (2) a technology track (co-led by Heyn and Jay Shin) identifying and scaling spatial genomics methods; (3) data analysis and storage infrastructure; and (4) public data portals enabling visual browsing and download.

---

## Section 2: Spatial Transcriptomics at Whole-Transcriptome Scale — Colorectal Cancer Case Study

Heyn described a collaboration with the (formerly NanoString, now Bruker) CosMx Spatial Molecular Imager, using **whole-transcriptome spatial profiling** (~18,000 genes per section) to map the continuum from healthy colon to colorectal cancer (CRC).

The experiment's design was elegant: a single tissue section from a CRC patient contained healthy colonic mucosa, pre-malignant polyp, and frank CRC regions within the same slide — spanning the full disease trajectory simultaneously. Cell type annotation (epithelial, immune, stromal) was performed using the transcriptome data, followed by sub-clustering to resolve cell states at higher resolution.

**Pseudotime trajectory analysis** — borrowed from the single-cell genomics toolbox — was applied to the spatially resolved epithelial cells: cells were ordered computationally from the healthy mucosa endpoint through the polyp stage to the CRC endpoint, and this ordering was mapped back onto the tissue section, visualizing cancer evolution as a spatial-to-transcriptional gradient.

Key findings:

*Tumor microenvironment evolution along the trajectory:*
- At the healthy end: **plasma B cells** dominate the immune compartment — a homeostatic immune surveillance phenotype.
- At the CRC end: **tumor-associated macrophages (TAMs)** dominate — an immune-suppressive phenotype permissive to tumor growth.
- Stromal compartment: **cancer-associated fibroblasts (CAFs)** accumulate at the malignant end, replacing the healthy fibroblast population and providing structural support for tumor invasion.

*Pathway activity signatures in cancer cells (along the trajectory):*
- Enrichment of metabolic reprogramming, proliferation, and cancer-hallmark pathways at the CRC end; these signatures are largely absent in healthy mucosa cells.
- Ligand-receptor interaction analysis revealed that cancer cells at the end of the trajectory actively secrete pro-proliferative signals received by immune and stromal cells, and receive immune-suppressive signals in return.

**Crypt-level resolution:** Crypts are the functional epithelial units of the colon — stem-cell-containing structures that renew the epithelial lining. The data revealed cancer evolution not just at the section level but **within individual crypts**: some crypts showed the full transition from healthy to CRC within a single functional unit, providing an unprecedented view of the earliest spatial scale at which malignant transformation occurs.

Heyn emphasized that whole-transcriptome profiling (vs. targeted gene panels) was essential for this analysis: it enabled unbiased cell state classification, trajectory inference, and pathway analysis without prior hypothesis about which genes to measure.

---

## Section 3: STAMP — Single-Cell Profiling Using Spatial Imaging Devices

A creative methodological contribution from Heyn's group is **STAMP (Spatial Transcriptomics of Adherent Monolayers for Profiling)** — repurposing spatial transcriptomics imaging instruments to profile cells in suspension (rather than tissue sections) at dramatically reduced cost.

**The core idea:** Imaging-based spatial transcriptomics instruments are extremely powerful but designed for tissue sections. Cells in suspension — such as peripheral blood mononuclear cells (PBMCs) — can be deposited as a monolayer on a standard glass slide and profiled with the same imaging protocols. Because the readout is imaging rather than sequencing, the cost per cell drops approximately 100-fold (sequencing is removed from the equation). Instead of sequencing indexed cell barcodes, cells are identified and transcriptomically profiled by direct imaging of RNA molecules.

**Performance and applications:**
- **Scale:** Up to 3 million cells per glass slide; up to 96 samples per slide by subdividing into sub-compartments (STAMP substamps)
- **Multimodality:** Imaging provides H&E morphology, immunofluorescence protein markers, and RNA simultaneously. Integration with Phenocycler Fusion (Akoya) enables co-detection with high-plex protein panels.
- **Rare cell detection:** Demonstrated detection of spiked cancer cell lines (~300 cells) within 2 million PBMCs — equivalent to 0.015% of the sample — by combining morphological features (larger cells) with transcriptomic cancer signatures and specific marker expression.
- **Clinical cohort profiling:** 96 samples per slide makes STAMP practical for large patient cohorts and longitudinal time-series experiments.

Compatible instruments include the CosMx (Bruker), Xenium and Terra (10x Genomics), with the Terra enabling full whole-transcriptome profiling of adherent cell monolayers.

STAMP represents an important cost-efficiency innovation: the same fundamental cell biology that single-cell sequencing interrogates can be accessed at a fraction of the cost when readout is by imaging, enabling the profiling of millions of cells per sample rather than tens of thousands.

---

## Section 4: Immune Repertoire Profiling — Cracking the Immune Code

The second major platform presented was Omniscope's immune repertoire profiling technology, described as "cracking the immune code." The conceptual foundation is that the immune system is a **natural sensor for disease**: T and B lymphocytes that recognize diseased cells (cancer, infected cells) expand clonally, and their TCR/BCR sequences serve as barcodes tracking which antigens the immune system has encountered and how it has responded.

**Scale as the enabling factor:** Omniscope profiles **1 million cells per sample**, compared to standard TCR/BCR sequencing methods that typically profile 10,000–100,000 cells. Heyn demonstrated that tracking clonotype dynamics over time requires this scale: at 10,000 cells, the connection between time points is largely lost; at 100,000 cells, it is weak; at 1 million cells, overlapping clonotypes between time points can be quantified with high precision.

Using Heyn's own blood profiled before and after COVID reinfection and a subsequent vaccination, the technology demonstrated:
- Identification of pre-existing clonotypes expanded by the infection (prior memory)
- De novo clonotypes newly recruited from the naive pool
- Tracking the conversion of newly activated clones to stable memory at a subsequent time point
- Re-amplification of natural infection-induced clonotypes by subsequent vaccination — validating that the vaccine "reads the same notes" as natural immunity

**Tumor-blood compartment tracking:** Up to 80–90% overlap between clonotypes present in tumor biopsies and those detectable in blood when profiling at scale, enabling blood as a **liquid immune biopsy** to track what is happening in the tumor without repeated invasive biopsies.

**Alpha-beta chain pairing:** Profiling both chains of the T-cell receptor (necessary to predict antigen specificity and for engineering TCR-T (TCRT) cell therapies) is supported at scale, enabling the pairing information needed for both experimental validation and clinical cell therapy design.

---

## Section 5: Clinical Applications — Colorectal Cancer Trial and Pediatric Rhabdoid Tumor Case

**Colorectal Cancer Clinical Trial (AstraZeneca/Valdebron Institute of Oncology):**

Heyn described a clinical trial in MSI-high (microsatellite instability-high) colorectal cancer patients treated with combined checkpoint inhibitor therapy (CTLA-4 + PD-L1 inhibition, AstraZeneca). Key results:

- **Responding patients:** Checkpoint inhibitor treatment produced a massive polyclonal T-cell response — both expansion of pre-existing tumor-reactive memory clones and de novo recruitment of new clonotypes.
- **Blood-tumor tracking:** Clonotypes expanding in blood after treatment were the same clonotypes that infiltrated the tumor post-treatment — directly demonstrating that the peripheral immune response is driving tumor clearance.
- **Predictive biomarker:** A **T-cell activity score** (derived from clonotype expansion frequency and proliferative dynamics) measured from blood two weeks after treatment start predicted which patients would respond to therapy (green responders vs. red non-responders). This very early blood-based read-out predicts long-term clinical outcome.

**Pediatric Rhabdoid Tumor Case Study:**

Rhabdoid tumors are pediatric tumors with very poor prognosis. A six-month-old child presented with a renal rhabdoid tumor with multiple metastases and high PD-L1 expression on tumor cells. Decision: chemotherapy plus checkpoint inhibitor therapy for one year; immune profiling-guided extension of immunotherapy for a second year based on observed immune dynamics.

Three years later: the patient is **tumor-free**.

Key observations from the immune profiling:
- Pre-treatment: predominantly T-regulatory cell expansion in blood (immunosuppressive)
- Post-treatment (early): CD8+ cytotoxic T-cells dominate the blood signal, representing the therapeutic immune response
- Late time points: CD4+ T-helper cells become the dominant expanding compartment, likely contributing to durable immune memory
- 13 of 19 major expanding clonotypes are still detectable at high frequency one year post-treatment — evidence of long-term immune memory formation

Validation of tumor reactivity: candidate TCR sequences identified from both blood and tumor were shown to directly kill tumor cell lines in co-culture experiments, validating them as tumor-reactive and as candidates for TCRT cell therapy design.

**ImmuneGPT:** Heyn described a foundation model of the immune system — built on Omniscope's database of millions of cells from thousands of individuals across healthy aging, cancer, infectious disease, and autoimmune contexts — as a browsable AI model for both diagnostic and therapeutic purposes. Applications include:
- Identifying T-cell receptors reactive against specific cancer types or molecular targets
- Identifying self-reactive T-cell receptors driving autoimmune pathology
- Predicting therapeutic response and stratifying patients for immune checkpoint inhibitor therapy

---

## Summary

Holger Heyn presented one of the most technically dense and clinically ambitious talks of the summit, spanning four interconnected topics: the HCA's transition to a spatially resolved, disease-inclusive, globally representative second phase; whole-transcriptome spatial profiling of colorectal cancer progression; a novel cost-efficient single-cell platform (STAMP) achieving million-cell scale at 100× cost reduction; and immune repertoire profiling at a scale sufficient to predict therapy response and guide clinical decision-making.

The unifying concept across all four sections was **scale enabling qualitative insight** — not just more data, but data at sufficient depth and resolution to answer questions that were previously unanswerable. In spatial transcriptomics, whole-transcriptome panels (vs. targeted 100-gene panels) enabled unbiased trajectory inference and cell-cell communication analysis. In immune repertoire profiling, profiling a million rather than ten thousand cells preserved the dynamic range needed to track clonotype changes over time and across tissue compartments.

The most compelling clinical demonstration was the pediatric rhabdoid tumor case: a child with a cancer whose general prognosis is poor, now tumor-free three years after treatment guided in part by immune profiling data. This was paired with the colorectal cancer data showing a blood-based T-cell activity score two weeks post-treatment as a predictor of long-term therapy response — a clinically actionable early biomarker directly enabled by the scale of immune profiling.

Heyn's framing of the immune system as a **natural sensor and natural therapy** for disease — one that evolution has optimized over 500 million years — provides a compelling conceptual unification for why immune profiling at scale is not just another -omics layer but a fundamentally different class of diagnostic and therapeutic resource. The ImmuneGPT foundation model represents the ambition to systematize this resource: a browsable map of immune state space that connects molecular measurements to clinical outcomes across disease contexts.
