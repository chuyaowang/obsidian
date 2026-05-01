# Conference Synthesis: State of Multi-omics and NGS 2026

**Event:** State of Multi-omics and NGS Virtual Summit  
**Organizer:** GEN (Genetic Engineering & Biotechnology News)  
**Exclusive Sponsor:** Illumina  
**Date:** 2026  

**Speakers:**
- Miranda Orr, PhD — Washington University School of Medicine *(Keynote)*
- Noorsher Ahmed, PhD — Stanford University (Lundberg Lab)
- Chris Dwan — Independent consultant / former Broad Institute, Semaphore
- Eric Green, MD, PhD — Chief Medical Officer, Illumina
- Bodour Salhia, PhD — Keck School of Medicine, USC
- Keith Robison, PhD — Ginkgo Bioworks / OmicsOmics blog
- Shawn Baker, PhD — SanDiegOmics
- Holger Heyn, PhD — CNAG Barcelona / Omniscope

---

## Overview

The State of Multi-omics and NGS 2026 Summit brought together researchers, clinicians, industry leaders, and data scientists to assess where the field stands across biological discovery, technology development, clinical translation, and data infrastructure. Six sessions spanned the full arc from fundamental neuroscience (spatial multiomics in Alzheimer's disease) to functional genomics at scale (optical pooled CRISPR screening), data management philosophy, multi-omics strategy and policy, NGS market dynamics, and single-cell and immune profiling at clinical scale.

Across all six talks, a coherent set of recurring themes emerged — some consensual, others openly contested — that together define the intellectual landscape of multi-omics and NGS in 2026.

---

## Theme 1: The "More Data" Paradox — Quality and Depth vs. Volume

The most persistent and philosophically interesting tension across the summit was between the drive to collect larger and more diverse datasets and the recognition that more data is only useful if it is of sufficient quality, resolution, and biological relevance.

Miranda Orr (Keynote) framed this most explicitly. Her lab learned more about tau pathology in Alzheimer's disease from **87 proteins than from 18,000 transcripts**, and more from **8 brains profiled with 1,200 proteins** than from **180 brains profiled with 87 proteins**. Her 3D serial-section experiment showed that RNA is undercounted by approximately 60% in single-section analyses of complex neurons — raising the question of how much spatial transcriptomic data collected from postmortem brain tissue actually reflects *biology* versus sampling artefact. Her call was for "complete data" and "higher fidelity data" rather than simply more data, and she advocated for deliberate ground-truth experiments to benchmark data quality before building AI models at scale.

Noorsher Ahmed arrived at the same conclusion from a different direction. Perturb-seq whole-genome screens produce enormous transcriptomic datasets, but because the transcriptome correlates poorly with the proteome, and because rare but biologically critical phenotypes (protein aggregation, mislocalisation, stress granule formation) are invisible to RNA-seq, the field risks optimising for dataset size rather than biological informativeness. His Optical Pooled CRISPR Screening platform is partly a response to this: cheaper, morphological readouts targeted at phenotypes that are actually mechanistically relevant to disease.

Chris Dwan made the same point from a data governance perspective. AI-generated synthetic data are not observations of the world; treating them as primary data corrupts the knowledge base on which future models are trained. His TCGA four-level framework is a tool for forcing researchers to be honest about what they have actually measured versus what they have inferred — a distinction that becomes critical when integrating data across modalities with different levels of processing.

The NGS Hot Goss panelists (Robison and Baker) raised the specific concern that multi-omics could devolve into "stamp-collecting" — accumulation of multimodal data without a hypothesis or analytical framework capable of extracting insight. Both were cautiously optimistic that longitudinal proteomics studies in particular will prove their worth, but both noted that the complexity of the proteome ensures that this layer of biology will "stay complicated for a really long time."

**Convergence point:** The consensus — implicit across all six talks — is that the field is moving from a phase of technological capability-building (can we measure this?) to a phase of biological interrogation (should we, and if so how?). The dominant bottleneck is no longer the generation of data but the depth of understanding with which it is interpreted.

---

## Theme 2: Protein Is Closer to Biology Than RNA — A Recurring Finding

Several speakers, working on entirely different problems, independently arrived at the primacy of protein-level measurement over transcriptomic measurement for understanding cellular function.

Orr's lab: "We've actually learned more about tau pathology using 87 proteins than 18,000 transcripts." Protein measurement in spatial experiments is also more stable across serial sections than RNA, and protein markers provide the cell boundary information necessary to correctly assign transcripts to cells in 3D reconstructions.

Ahmed: Morphological phenotypes detectable by imaging (which reflect protein-level cellular architecture, localisation, and dynamics) capture disease-relevant states that are invisible to transcriptomics. His explicit argument that "the transcriptome does not correlate well with the proteome" is a theoretical underpinning of the shift toward optical pooled screening.

Green and Salhia: Salhia specifically highlighted the challenge of capturing how DNA methylation *controls* gene expression — a regulatory relationship that operates at the protein level (transcription factors, chromatin modifiers) and is not directly readable from RNA.

Robison and Baker: The proteomics opportunity — serum protein profiling in longitudinal cohorts, mass spectrometry, Olink-type proximity extension assays — was identified as the most biologically exciting expansion of multi-omics beyond DNA sequencing, precisely because the proteome is closer to cellular activity than the transcriptome.

Heyn: The STAMP platform is explicitly designed to add protein profiling (immunofluorescence and high-plex antibody panels) alongside RNA in single-cell imaging assays, recognizing that morphology and protein markers provide complementary information that RNA alone cannot supply.

**Convergence point:** Protein measurement is emerging as the critical underserved dimension of multi-omics. Transcriptomics had a first-mover advantage because RNA-seq was accessible and scalable before proteomics; the field is now correcting this imbalance. The TCGA-era multi-omics framework (genome + transcriptome + methylation) is being expanded to systematically include spatial proteomics.

---

## Theme 3: 3D, Spatial, and Temporal Dimensions — Moving Beyond the 2D Snapshot

Multiple talks converged on the inadequacy of two-dimensional, single-time-point molecular measurements for capturing the biology of complex systems.

Orr's serial-section experiment is the most direct demonstration: reconstructing neurons in 3D revealed that approximately 60% of their transcript content is invisible in any single 2D section. For biologically complex, large cells — neurons, senescent cells — 3D reconstruction is not a luxury but a prerequisite for accurate molecular characterization. The finding that senescent nuclei can expand tenfold relative to healthy cells suggests that many senescent neurons currently profiled in 2D are being fundamentally misrepresented.

Heyn's HCA 2.0 roadmap explicitly includes the transition from 2D spatial atlases to 3D organ-level reconstructions, acknowledging that tissue architecture is inherently three-dimensional and that the regulatory relationships between cells depend on their spatial relationships in all three dimensions.

Heyn's immune profiling work adds the **temporal** dimension: tracking T-cell clonotypes over time (pre-infection, post-infection, post-vaccination; pre-treatment, multiple cycles of therapy) is what reveals the dynamic immune response that drives clinical outcomes. Static snapshots of the immune repertoire are insufficient to distinguish recently activated clones from pre-existing memory, or to track tumor-specific immunity as it evolves under therapy pressure.

Salhia's discussion of temporal multi-omics — measuring how methylation regulates gene expression *over time* as cells respond to stimuli — identified temporal dynamics as one of the most underappreciated dimensions in current multi-omics frameworks.

**Convergence point:** The field is moving toward a four-dimensional view of biology: space (x, y, z) plus time. The enabling technologies (serial sectioning + 3D reconstruction, time-lapse spatial profiling, longitudinal liquid biopsy) are becoming available. The analytical frameworks for 4D data integration are still maturing.

---

## Theme 4: AI as Tool, Not Oracle — The Interpretability Problem

Every speaker discussed AI, and every speaker expressed a version of the same nuanced position: AI is genuinely transformative as an analytical and operational tool, but it is not a substitute for domain expertise, it is not reliable as a generator of primary scientific data, and its outputs require validation against biological ground truth.

Orr raised the concern most forcefully: if foundation models are trained on spatial transcriptomics data from postmortem tissue that systematically underrepresents transcript content due to 2D sampling of 3D cells, the models will encode those artefacts as features rather than noise. "The potential to compound an issue if the data generated aren't robust" is an institutional risk to the entire field, not just individual labs.

Dwan drew a categorical distinction: AI outputs are not data. They are useful for imputation, pattern recognition, and hypothesis generation, but they are not observations of the world and must not be treated as Level 2 archival data in the TCGA sense. He also identified the natural language interface to data (LLM-mediated SQL-equivalent queries) as transformative for accessibility — enabling non-computational scientists to interact with their own data without technical intermediaries — while cautioning that accessibility without domain expertise will produce turbulence.

Green and Salhia articulated the requirements for trusting AI in translational contexts: interpretability (outputs traceable to biological mechanisms), validation in real-world datasets representative of clinical populations, and training data quality ("garbage in, garbage out"). Salhia noted that AI model failures in translational genomics are more common than reported because they happen quietly — researchers don't always publish negative AI results.

Ahmed built an AI layer into his perturbation biology platform (agentic screen design using graph RAG with specialist sub-agents, supported by Anthropic) specifically to address the mathematical limits of brute-force whole-genome perturbation screening. This is an example of AI used intelligently within its domain of competence: generating experimentally tractable hypotheses from biological knowledge graphs, not generating data.

Heyn's **ImmuneGPT** represents a foundation model built on a carefully curated, domain-specific dataset (millions of cells from thousands of individuals with rich clinical annotation), designed to be browsable for targeted diagnostic and therapeutic queries. This is the model for how biological foundation models should be built: domain-specific, well-annotated, and evaluated against clinical outcomes rather than benchmark performance.

**Convergence point:** The summit's collective position on AI is best summarized as "intelligent tool use requiring domain expertise." AI accelerates analysis, enables scale, and opens new windows of inquiry — but the quality of its outputs is bounded by the quality of its inputs, and the interpretability of its outputs requires the same biological knowledge that has always been required to interpret experimental data.

---

## Theme 5: Clinical Translation — Oncology Leads, But the Path Is Clear for Other Fields

Clinical translation of multi-omics and advanced genomics was a thread running through multiple sessions, with oncology consistently identified as the leading application domain and other disease areas positioned as emerging opportunities.

Orr's work on Alzheimer's disease represents an effort to use spatial multiomics to understand the cellular mechanism of neurodegeneration at a level of resolution sufficient to design rational senolytic therapies. Her lab has already run a Phase 2 clinical trial testing senescent cell clearance in mild cognitive impairment / early AD — a direct translation of the tangle-senescence hypothesis.

Green's MOHD consortium is explicitly designed to demonstrate multi-omics value in human disease contexts beyond cancer — rare genetic diseases, complex common disorders — with the stated goal of convincing other NIH institutes to invest in multi-omics infrastructure.

Heyn's immune profiling work in a pediatric rhabdoid tumor case is perhaps the summit's most powerful clinical demonstration: immune repertoire data guided the extension of immunotherapy for a second year in a child with a universally poor-prognosis cancer, who remains tumor-free three years later. This is not a population statistic but a case that illustrates how multi-omics can contribute to clinical decisions in individual patients — n-of-1 medicine.

Salhia's ovarian cancer biomarker work represents a canonical translational pipeline: tissue multi-omics to identify relevant biology, plasma proteomics to develop a liquid biopsy proxy, spatial validation to understand tissue context, classification algorithms to enable clinical deployment.

The NGS market discussion highlighted the structural economic driver: Illumina's clinical revenue now constitutes ~60% of total sequencing revenue. Roche Axelios enters specifically targeting the clinical laboratory market, with speed (NICU rapid diagnosis), reusable chip economics, and Roche's global diagnostic infrastructure as competitive advantages.

**Convergence point:** Clinical application of multi-omics is not a future vision but an emerging reality, primarily in oncology and rare disease. The trajectory of sequencing — from research tool to clinical standard — is being recapitulated for multi-omics, with perhaps five years before routine multi-modal clinical tests exist in cancer and potentially other fields.

---

## Theme 6: Data Infrastructure as a Strategic Imperative

Dwan's dedicated session on data management, combined with threads from other speakers, identified data infrastructure as an underinvested and often neglected aspect of multi-omics programs.

Dwan's core argument — that domain expertise is the irreducible prerequisite, that someone must own data governance with cross-cutting authority (the Data Czar), and that data management is fundamentally a human organizational problem that technology cannot solve — was echoed implicitly in other talks. Orr's concern about building AI models on low-fidelity postmortem tissue data is a data quality problem. Heyn's HCA investment in data portals, metadata standards, and analysis tool ecosystems is a data infrastructure problem. Ahmed's packaging of all OPS data into AnnData format (compatible with the single-cell analysis ecosystem) is a data standards decision.

Salhia's observation that data harmonization across modalities is still one of the hardest problems in multi-omics — even with improved platforms — points to the same challenge: multi-omics is only as good as the infrastructure that allows its constituent layers to be analyzed in combination.

Green's observation that a natural language interface to structured data (LLM-mediated querying) is "transforming the ability to get access across disciplines" identifies the near-term leverage point: the democratization of data access is already here; the challenge is using it without generating more noise than signal.

**Convergence point:** As multi-omics matures from a specialist activity to a broadly deployed scientific infrastructure, the gap between data generation and data management is becoming the limiting factor. The organizations that invest in data governance, metadata standards, accessible portals, and skilled data management personnel will extract more value from their multi-omics investments than those that treat data management as an IT problem rather than a scientific one.

---

## Theme 7: Scale Enables Qualitative Insight — The Non-linear Relationship Between N and Discovery

A quieter but important theme: in several cases, scaling the number of cells profiled, sections analyzed, or proteins measured did not merely improve statistical power but **qualitatively changed what questions could be asked and answered**.

Heyn's immune profiling at 1 million cells per sample vs. 10,000 or 100,000 does not just provide more statistical confidence in the same clonotype tracking analysis; at lower depths, the connection between time points is simply lost. The dynamic range required to track rare clonotypes expanding against a background of millions of cells is only achievable at scale.

Orr's 3D serial-section approach does not just add confidence to 2D transcript measurements; it reveals spatial patterns of transcript distribution within cells that are invisible in 2D, and identifies that transcript-count differences between 2D and 3D are consistent (~2-fold increase, not random noise), implying systematic under-measurement rather than sampling variability.

Ahmed's whole-genome OPS screens do not just add statistical power to targeted screens; they can reveal unexpected biological connections between genes in different parts of the interaction network that targeted screens by definition cannot find.

**Convergence point:** Scale in multi-omics is not simply a matter of statistical adequacy — it is often the threshold below which certain phenomena are qualitatively inaccessible. This has implications for study design: it is possible to produce datasets that are statistically underpowered not just in the classical sense but in the deeper sense of lacking the dynamic range to observe the phenomenon of interest at all.

---

## The Competitive and Commercial Landscape

The summit was partially shaped by its sponsorship context (Illumina), which became visible in the explicit discussion of Illumina's vertical integration strategy, the MOHD consortium launched under Green's NHGRI tenure, and the framing of multi-omics as a business opportunity. This context should be noted.

The NGS Hot Goss session offered the most unvarnished market perspective: Illumina's dominance (77–78% market share) has proven more durable than many expected; the multi-omics commercial strategy is a rational response to saturating research markets; and Roche Axelios is the most significant new clinical entrant in years, with genuine technological differentiation (speed, flexible throughput economics, Roche's clinical infrastructure) but with first-generation limitations.

The broader competitive dynamic — multiple companies positioning multi-omics capability as a differentiator (Illumina's one-stop-shop vs. specialized partners) — reflects a fundamental question about whether multi-omics will be served by integrated platform vendors or by modular ecosystems of specialized tools. Both speakers suggested the answer will be determined by clinical practicality: clinical labs want simplicity, while research labs want flexibility.

---

## Looking Forward: What the Summit's Collective Agenda Suggests

The summit's speakers, taken together, suggest that the multi-omics field in 2026 is at an inflection point characterized by:

**Maturation of enabling technologies.** Spatial multiomics at whole-transcriptome scale is now commercially available and being deployed at scale (HCA, academic labs, pharma). Protein profiling at >1,000-plex is accessible. Immune profiling at million-cell scale is achievable. The technology gaps of five years ago are largely closed.

**The analytic and interpretive frontier.** The hardest problems are now computational and conceptual: how to integrate data across modalities and scales, how to build AI models that are biologically grounded and clinically validated, how to extract causal rather than correlative insight from observational multi-omics data, and how to manage the transition from bulk tissue to single-cell to 3D spatial to temporal multi-omics without losing data fidelity.

**The clinical translation race.** Oncology is already deploying multi-omics-derived biomarkers in research trials. Rare disease genomics is expanding into multi-modal approaches. Neurodegenerative disease (Alzheimer's in particular) is accumulating the biological understanding necessary for rational therapy design. The field should expect a small number of validated clinical multi-omics tests within five years, with broader adoption following on the standard technology diffusion curve.

**The data infrastructure debt.** Every organization generating multi-omics data at scale faces a version of Dwan's challenge: managing, integrating, securing, and making accessible data that was generated across platforms, time points, and disciplines without a coherent organizational framework. The organizations that solve this problem will extract compounding scientific value; those that don't will continue generating increasingly expensive datasets whose insights remain locked in lab notebooks and unindexed file systems.

**Responsible data generation.** Orr's call for "responsible generation of data" — not generating data just because we can, but ensuring data fidelity and biological relevance before deploying AI at scale on those data — is the summit's most uncomfortable message and perhaps its most important. It asks the field to slow down at exactly the moment when it has the most technical capability to go fast.

The 2026 summit left the strong impression of a field that is scientifically excited, commercially competitive, and technically capable — and that is now, for the first time, genuinely limited more by the depth of its biological understanding and the quality of its analytical frameworks than by the power of its instruments.
