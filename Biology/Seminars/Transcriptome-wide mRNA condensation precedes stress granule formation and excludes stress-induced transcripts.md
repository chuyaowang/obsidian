# Transcriptome-wide mRNA condensation precedes stress granule formation and excludes stress-induced transcripts

#paper 
#smFISH
[link](https://www.biorxiv.org/content/10.1101/2024.04.15.589678v2.full)

## Motivation

Cells exposed to sudden stresses must reprogram protein synthesis and transcription to survive. Although stress granules (SGs)—membraneless condensates of mRNA and proteins—are conserved across eukaryotes, their formation mechanisms and relationship to transcriptional responses remain unclear. This study aims to dissect the earliest stages of mRNA condensation under stress and understand how cells prioritize translation of newly synthesized transcripts.

## Research question

What are the sequence– and length‐independent mechanisms driving mRNA condensation during stress, and how does this condensation affect the selective translation of stress‐induced mRNAs?

## Background

- Stress granules form after translation initiation is blocked, recruiting untranslated mRNAs and initiation factors but excluding nascent transcripts.
- The “ribosome-free RNA template” model posits that exposed mRNA drives SG assembly via multivalent RNA–RNA or RNA–protein interactions.
- Prior high‐throughput studies linked mRNA length to SG recruitment, but early anecdotal reports suggested stress‐induced transcripts escape SGs.

> [!note]- Stress granules and significance
> ### What Are Stress Granules?
> 
> Stress granules are transient, membraneless assemblies of RNA and protein that form in the cytoplasm of eukaryotic cells when environmental or physiological stress disrupts normal translation. Key features include:
> 
> - Enrichment of untranslated messenger RNAs bound by RNA-binding proteins (e.g., poly(A)-binding protein Pab1 in yeast) and stalled translation initiation complexes
> - Exclusion of nascent transcripts produced during the stress response
> - Formation downstream of translation initiation inhibition, ribosome run-off, and exposure of ribosome-free mRNA
> - Appearance as visible foci under the microscope when labeled with markers such as Pab1 or poly(A)+ RNA
> 
> These condensates arise by phase separation driven by multivalent RNA–RNA and RNA–protein interactions, with contributions from both RNA length and specific interaction domains on proteins.
> 
> ---
> 
> ### Significance of Stress Granules
> 
> Stress granules play several critical roles in cellular homeostasis and disease:
> 
> - Translation Regulation  
>     By sequestering nonessential mRNAs and initiation factors, stress granules globally downregulate protein synthesis, conserving resources under adverse conditions.
>     
> - mRNA Triage and Protection  
>     They serve as hubs to sort transcripts: house-keeping mRNAs are stored, while stress-response transcripts remain accessible for translation.
>     
> - Cellular Signaling and Adaptation  
>     Granule assembly and disassembly integrate signaling pathways (e.g., eIF2α phosphorylation), coordinating transcriptional and translational programs during recovery.
>     
> - Principles of Biomolecular Condensation  
>     As paradigms of phase-separated compartments, stress granules illuminate how cells organize without membranes, highlighting the roles of multivalency and low-complexity domains.
>     
> - Disease Implications  
>     Aberrant or persistent stress granules are linked to neurodegenerative disorders—such as amyotrophic lateral sclerosis and frontotemporal dementia—where misregulated RNA–protein condensates contribute to pathology.
>     
> 
> Understanding stress granules thus provides insights into fundamental cell biology, stress adaptation strategies, and potential therapeutic targets in diseases of protein-RNA aggregation.


### Data type and acquisition

- Yeast (Saccharomyces cerevisiae) cultures under no stress (30 °C), mild (42 °C) and severe (46 °C) heat shock; sodium azide; ethanol treatments.
- Biochemical fractionation (Sed‐seq): cell lysis, sedimentation to separate condensed (pellet) and soluble (supernatant) fractions, followed by RNA sequencing.
- Single‐molecule FISH (smFISH) for colocalization of specific mRNAs with SG marker Pab1.
- Polysome profiling (Polysome‐seq) to assess ribosome association.
- Reporter constructs under tetracycline control to decouple sequence features from expression timing.

> [!note]- Polysomes
> ### What Are Polysomes?
> 
> Polysomes, or polyribosomes, are assemblies of multiple ribosomes simultaneously translating a single messenger RNA (mRNA) molecule. Each ribosome binds at the 5′ end of the mRNA and moves toward the 3′ end, synthesizing polypeptide chains in parallel. This multiribosome configuration enables efficient and high-throughput protein production from one mRNA template.
> 
> #### Formation and Structure
> 
> - After initiation of translation, the first ribosome vacates the mRNA’s start site, allowing another ribosome to bind.
> - As translation proceeds, additional ribosomes “stack” behind the leading ones, forming a “beads-on-a-string” arrangement when visualized by electron microscopy.
> - The number of ribosomes per mRNA varies with transcript length, codon usage, and translation rate.
> 
> #### Biological Significance
> 
> - Polysomes are direct indicators of active translation: more ribosomes per mRNA generally reflect higher protein synthesis rates.
> - Cells regulate polysome assembly in response to environmental cues—nutrient availability, stress conditions, or signaling pathways—to control protein output.
> - Disruptions in polysome dynamics can lead to aberrant protein production, implicated in diseases such as cancer and neurodegeneration.
> 
> #### Measurement of Polysomes
> 
> 1. Sucrose Gradient Centrifugation
>     
>     - Cell lysates are layered onto a linear sucrose gradient and ultracentrifuged.
>     - Heavier polysomes sediment deeper, separating by ribosome count.
>     - Absorbance profiles at 254 nm (A254) reveal peaks for monosomes (80S) and polysomes.
> 2. Polysome-seq
>     
>     - Fractions from sucrose gradients are collected and sequenced.
>     - Reads mapping to transcripts quantify ribosome association on each mRNA genome-wide.
>     - Enables comparison of translation efficiencies across conditions.
> 
> #### Role in the Study
> 
> In the discussed paper, Polysome-seq data correlated transcript-specific changes in ribosome occupancy with their propensity to condense into stress-induced assemblies. Transcripts gaining ribosomes under stress tended to escape condensation, linking active translation to condensate partitioning.
> 
> ---
> 
> #### Beyond Polysomes
> 
> - Ribosome profiling (Ribo-seq) offers codon-level resolution of ribosome positions on mRNAs.
> - In stress biology, polysome collapse (shift from polysomes to monosomes) signals global translational repression.
> - Single-molecule imaging techniques (e.g., SunTag) can visualize polysome dynamics in living cells.

## Theoretical framework

- **Biomolecular condensation**: phase‐separation driven by multivalent interactions among RNA and proteins, creating concentrated foci without membranes.
- **Universal trigger model**: stress‐induced polysome disassembly exposes ribosome‐free mRNAs that nucleate SGs.
- **Temporal escape model**: newly transcribed mRNAs during stress avoid condensation due to delayed multivalent interactions.

## Methods

1. Sed‐seq
    - Added EDTA to disrupt polysomes.
    - Bayesian mixture model to estimate each transcript’s proportion in supernatant (pSup) and compute length‐corrected Z score (sedScore).
2. smFISH colocalization
    - Probing induced (e.g., SSA4, HSP104) vs. uninduced (e.g., SSB1, ADD66) mRNAs.
3. Polysome‐seq
    - Quantified stress‐dependent changes in ribosome association per transcript.
4. Reporter assays
    - TET‐inducible transcripts with UTRs from HSP26 (stress‐induced) or PMU1 (unstressed).
    - Measured condensation (qPCR) and ribosome occupancy (sucrose‐cushion).
5. Translation initiation blockade
    - Auxin‐inducible degron on eIF3b to inhibit initiation, testing condensation in absence of ribosome release.

> [!note]- Sed-seq
> 
> ### What Sed-seq Measures
> 
> Sed-seq provides a transcriptome-wide, unbiased readout of mRNA condensation into dense, insoluble assemblies. By comparing pSup and sedScore across conditions, it reveals how each mRNA partitions between a soluble pool and condensed structures—capturing early, pre–stress granule condensation events that are invisible under the microscope.
> 
> ### Experimental Workflow
> 
> 1. Sample Preparation  
>     Yeast cells are harvested under control or stress conditions and lysed in buffer containing EDTA to disassemble polysomes.
>     
> 2. Fractionation by Centrifugation  
>     The lysate is spun at high speed to separate soluble components (supernatant) from dense, condensed assemblies (pellet).
>     
> 3. RNA Extraction and Sequencing  
>     RNA is isolated from total lysate, supernatant, and pellet fractions, then subjected to high-throughput RNA sequencing.
>     
> 
> ### Quantifying mRNA Partitioning
> 
> - Proportion in Supernatant (pSup)  
>     For each transcript, the fraction of reads in the supernatant versus total (supernatant + pellet) is computed. A low pSup indicates extensive sedimentation (condensation).
>     
> - Bayesian Mixture Modeling  
>     A statistical model infers each gene’s true pSup, adjusting for technical noise and sequencing depth.
>     
> - Relative Condensation (sedScore)  
>     pSup is converted to log-odds and normalized against transcripts of similar length to yield a Z-score (sedScore), isolating stress-induced changes from inherent length-dependent sedimentation.

## Results

- **Global mRNA condensation** occurs transcriptome‐wide under all stresses, independent of visible SG foci (Sed‐seq pSup decreases for nearly all mRNAs).
- **Length plays a minor role** once baseline sedimentation is corrected: short and long mRNAs condense similarly under stress.
- **Stress‐induced transcripts escape condensation** (ΔsedScore > 0) in proportion to their induction level, across heat, azide, and ethanol stresses.
- **smFISH** confirms that induced mRNAs (SSA4, HSP104) localize outside Pab1‐marked SGs, while uninduced mRNAs colocalize.
- **Translation correlates with escape**: transcripts with increased ribosome association under stress tend to avoid condensation.
- **Timing, not sequence**, drives escape: reporter mRNAs newly transcribed during stress remain soluble regardless of UTR sequence.
- **Initiation blockade** (eIF3b depletion) induces mRNA condensation (TIICs) even without ribosome release, yet newly made transcripts still escape condensation.

## Key Figures and Tables

|Figure|Description|
|---|---|
|1A–E|Schematic of Sed‐seq; heat shock induces transcript condensation; pSup vs. length; introduction of sedScore metric.|
|1F–H|Example transcripts (HSP104 vs. PMU1) show different ΔsedScore; simple two‐parameter model fits length‐independent interactions; comparison to prior SG data.|
|2A–C|Induced transcripts escape condensation; smFISH images and colocalization quantification for SSA4, HSP104, SSB1, ADD66.|
|3A–E|Condensation across stresses (heat, azide, ethanol); top 100 induced mRNAs highlighted; Polysome‐seq vs. Sed‐seq correlation.|
|4A–E|Reporter assay: old vs. new transcripts; eIF3b depletion effects; ribosome occupancy vs. condensation findings.|

## Validations

- qPCR and spike‐in controls confirm Bayesian pSup estimates.
- Concordance of Sed‐seq with smFISH and Polysome‐seq data.
- Auxin‐induced eIF3b degradation validated by Western blot and polysome collapse.
- Reporter constructs eliminate confounding UTR features, isolating timing effects.

## Implications

- **Mechanistic insight**: mRNA condensation begins as translation initiation‐blocked condensates (TIICs) before visible SGs.
- **Cellular strategy**: pre‐existing mRNAs are sequestered to free translation machinery for stress‐response transcripts.
- **Revised paradigm**: length‐dependent SG recruitment is overestimated; timing of transcript synthesis is primary determinant of partitioning.

## Clinical relevance

Although this is a yeast study, understanding mRNA condensation has implications for human diseases linked to SG dysfunction—such as amyotrophic lateral sclerosis and frontotemporal dementia—where aberrant condensates contribute to neurodegeneration. Targeting initiation steps or modulating transcript timing could inform therapeutic strategies.

---

Further exploration could include single‐molecule real‐time imaging of TIICs, extending findings to mammalian systems, and investigating how condensate dynamics influence recovery from stress and cellular aging.

---

## smFISH Provides Orthogonal, Single-Cell Spatial Validation

smFISH (single-molecule fluorescence in situ hybridization) complements the global Sed-seq data by directly visualizing individual mRNA molecules in intact cells. Here’s what it uniquely adds:

- Precise colocalization of transcripts with condensates  
    smFISH lets the authors label specific mRNAs (e.g., SSA4, HSP104, SSB1, ADD66) and simultaneously mark stress granules via Pab1. This spatial pairing confirms which transcripts enter or are excluded from granules, validating the sedimentation-based partitioning at the level of single molecules.
    
- Confirmation of length-independent escape  
    By picking long and short mRNAs with different induction profiles, smFISH shows that exclusion from granules tracks stress-induction, not transcript length. This concrete imaging evidence resolves potential confounders in high-throughput analyses.
    
- Quantitative colocalization metrics  
    The authors calculate a per-cell “colocalization score” by comparing Pab1 signal intensity at mRNA foci versus random cytoplasmic regions. These measurements rigorously quantify the degree of enrichment or exclusion for each transcript.
    
- Visualization under different stress intensities  
    smFISH images under mild (no visible granules) and severe (clear granules) heat shocks demonstrate that induced mRNAs remain excluded even when condensates are microscopically invisible, supporting the notion of pre-granule TIICs.
    

Together, smFISH grounds the transcriptome-wide sedimentation results in spatial, single-molecule reality—eliminating ambiguities about cell-to-cell variability, confirming selective transcript partitioning, and underpinning the model that timing of transcription, not length or sequence, dictates condensation fate.

---

### Beyond This Study

- Multiplexed smFISH (e.g., MERFISH) could simultaneously track dozens of transcripts to map the full landscape of mRNA partitioning in stress.
- Live-cell RNA imaging using MS2/MCP tags would reveal the real-time kinetics of TIIC formation and transcript escape.
- Super-resolution methods (e.g., STORM) could dissect the nanoscale organization of TIICs versus mature stress granules.
