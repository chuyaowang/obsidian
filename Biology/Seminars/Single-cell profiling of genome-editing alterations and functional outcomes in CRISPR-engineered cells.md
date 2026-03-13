# Single-cell profiling of genome-editing alterations and functional outcomes in CRISPR-engineered cells

[link](https://watch.getcontrast.io/watch/missionbio-2-single-cell-profiling-of-genome-editing-alterations-and-functional-outcomes-in-crispr-engineered-cells)
#seminar 

**Speakers:**

* **Mike**, Senior Marketing Manager, Mission Bio
* **Adam Chernick**, Senior Commercial Product Manager, Integrated DNA Technologies (IDT)
* **Nechama Kalter**, PhD Student, Hendel Lab, Bar-Ilan University

---

## 1. Contextual Knowledge & Definitions

To fully appreciate the technical depth of this talk, the following concepts are essential:

* **CRISPR-Cas9 Gene Editing:** A technology allowing precise modification of DNA. It involves a guide RNA (gRNA) that directs the Cas9 enzyme to a specific genomic location (on-target) to create a double-strand break.
* **On-target vs. Off-target Effects:** *On-target* refers to the intended genetic modification. *Off-target* effects are unintended mutations at other genomic sites with similar sequences to the target, posing safety risks (genotoxicity).
* **Indels:** Small **In**sertions or **del**etions of bases in the DNA sequence, often resulting from the cell's repair of the Cas9-induced break.
* **Translocations:** Large-scale structural variants where chromosome segments break and reattach to different chromosomes.
* **Zygosity (Monoallelic vs. Biallelic):** Humans have two copies (alleles) of most genes. *Monoallelic* editing modifies only one copy; *biallelic* editing modifies both. For "knockout" therapies (disabling a gene), biallelic editing is often required for functional efficacy.
* **Bulk Sequencing vs. Single-Cell Sequencing:**
  * *Bulk:* Sequences DNA from a mixed population of cells, providing average frequencies (e.g., "50% of alleles are edited"). It cannot determine if one cell has two edited alleles or if two cells have one edited allele each.
  * *Single-Cell (e.g., Tapestry):* Analyzes DNA from individual cells, allowing determination of zygosity, co-occurrence of mutations (e.g., does the same cell have an on-target edit *and* an off-target edit?), and structural variants per cell.
* **Multi-omics:** The integration of different biological data types (e.g., genotype/DNA and phenotype/protein) from the same sample to understand cause-and-effect relationships.

---

## 2. Sectional Reports

### Section 1: The Standard for CRISPR Validation (Nomination & Confirmation)

**Speakers:** Mike (Mission Bio) and Adam Chernick (IDT)

**Challenges Resolved:**
The primary challenge addressed is the safety and reliability of CRISPR-based therapies. Specifically, researchers need to ensure that gene edits happen *only* where intended and that the edits function as designed without causing genomic instability. Relying solely on predictive algorithms or bulk sequencing fails to capture the full landscape of genotoxicity (genome damage) and functional efficacy at the cellular level.

**Methods & Workflow:**
The speakers proposed a three-step "Gold Standard" workflow for validating genome editing:

1. **Nomination (Discovery):** Identifying *where* in the genome the CRISPR system might accidentally cut (off-targets).
    * *Method:* IDT’s **UncoverSeq** (based on the GUIDE-seq method). This is an unbiased, cell-based assay. Cells are transfected with gRNA and a double-stranded DNA tag. The tag integrates into Double-Strand Breaks (DSBs). Sequencing locates these tags to identify potential off-target sites.
    * *Advancement:* IDT optimized the tag chemistry to increase integration rates, reportedly achieving a 10-fold increase in sensitivity compared to standard GUIDE-seq.
2. **Confirmation:** Verifying which of the nominated sites are actually modified in clinically relevant cells.
    * *Method:* IDT’s **rhAmpSeq** (RNase H2-dependent PCR). This is a high-throughput amplicon sequencing technology using chemically modified primers to multiplex (target many sites simultaneously) hundreds of loci in a single library.
    * *Outcome:* Provides quantitative data on indels and translocations at specific sites identified during nomination.
3. **Deep Confirmation:** Characterizing the functional outcome and complex genetic architecture per cell.
    * *Method:* Mission Bio’s **Tapestry Platform**. This microfluidic single-cell platform captures individual cells in droplets, digests chromatin to access DNA, and performs barcoding and targeted amplification.
    * *Outcome:* Links genotype (zygosity, co-occurrence) to phenotype (protein expression) and detects rare subclones that bulk methods miss.

**Transition:**
Having established the necessary workflow for safety (nomination/confirmation), the talk transitions to a real-world application of the "Deep Confirmation" step using the Tapestry platform, presented by Nechama Kalter.

### Section 2: Single-Cell Profiling of Genome Editing (The Study)

**Speaker:** Nechama Kalter (Hendel Lab, Bar-Ilan University)

**Context & Motivation:**
The Hendel Lab focuses on gene therapies for hematopoietic disorders, specifically Severe Combined Immunodeficiency (SCID). For a therapy to be safe and effective, they must maximize the population of cells with the correct *functional* edit (e.g., biallelic knockout) while minimizing cells with off-target mutations or dangerous chromosomal translocations.

**Study Design:**

* **Cell Type:** Primary Human T-cells (2 donors).
* **Targets:** Three genes adapted from a clinical trial (by Carl June): *TCRB* and *TCRA* (T-cell receptor components) and *PDCD1* (PD-1 immune checkpoint).
* **Timeline:** Cells were edited and sequenced at multiple time points (6h, 24h, 3 days, ~2 weeks).
* **Assays:** Validated single-cell DNA sequencing (Tapestry) against bulk sequencing (rhAmpSeq) for 3 on-target and 111 off-target sites.

**Key Results & Analysis:**

1. **Resolution of Zygosity (The "Allele" vs. "Cell" Problem):** Nechama demonstrated that bulk sequencing often misleads. In a theoretical example, "50% editing" in bulk could mean 100% of cells are mono-allelic (heterozygous) or 50% are bi-allelic (homozygous). Using single-cell data, they quantified the exact percentage of cells with **biallelic edits**, which is crucial because often only biallelic disruption leads to a complete functional "knockout" of the protein.
2. **Co-occurrence and "Target Population":** The goal was a "multiplex knockout" (disabling both TCR and PD-1). While simple biallelic editing rates seemed high, the strict "Target Population" (cells with biallelic *frameshift/null* mutations in both targets) was only **~13%**. This precise quantification is impossible with bulk methods, which would overestimate success by multiplying average efficiencies. They found that edits occurred independently; there was no significant dependency (one edit making another more likely).
3. **Genotoxicity & Off-Targets:** They tracked 111 nominated off-target sites. They identified one highly active off-target site (*TCRB-OT-51*). Crucially, they determined that **2%** of the therapeutic "Target Population" (the 13% successful cells) contained this off-target mutation. This reveals a specific risk profile for the therapeutic product that bulk sequencing implies but cannot quantify per cell.
4. **Translocations:** They searched for "chimeric reads" (DNA sequences fusing two different genomic regions) in both bulk and single-cell data. Single-cell data not only detected translocations (e.g., between *PDCD1* and *TCRB*) but quantified them (e.g., 0.55% frequency). They even detected a translocation not reported in the original high-profile scientific publication, demonstrating superior sensitivity.
5. **Genotype-Phenotype Correlation (Multi-omics):** They stained cells for TCR and CD3 proteins and sequenced the DNA of those same cells. They observed a clear negative correlation: as biallelic frameshift mutations increased over time, protein expression decreased. Time-course analysis showed translocations peaked around day 7 and then decreased, suggesting **negative selection**—the cells with severe genomic damage were dying off or being outcompeted, a vital insight for determining the optimal harvest time for cell therapies.

### Section 3: Q&A and Future Directions

**Future Technology:**
Mike announced a new Mission Bio capability: **Targeted Gene Expression Profiling**. This will allow simultaneous sequencing of DNA (mutations) and RNA (gene expression) from the same single cell, providing a more direct link between an edit and the cell's transcriptional state.

**Q&A Session Summary:**

* **Question:** Why was there a discrepancy between Tapestry (single-cell) and rhAmpSeq (bulk) data for the *PDCD1* gene?
  * **Answer (Nechama):** This was due to **primer design** and **large deletions**. The *PDCD1* guide induced large deletions (up to 100bp). If the sequencing primers land within the deleted region, the DNA fails to amplify, and the deletion is missed (allelic dropout), making the cell look "Wild Type." Optimizing primer placement to flank potential large deletion sites is critical for accuracy.
* **Question:** Single-cell sequencing is expensive. Why not just use bulk?
  * **Answer (Nechama):** Bulk is suitable for early screening. However, for clinical products, single-cell is necessary to see the "true diversity." It reveals co-occurrence (e.g., does the effective cell also have the dangerous mutation?) and zygosity, which bulk cannot provide.
* **Question:** Was there any dependency between edits (e.g., did editing Gene A help edit Gene B)?
  * **Answer (Nechama):** No. The observed co-occurrence frequencies matched the mathematical product of their individual probabilities, indicating independent editing events without clonal selection for specific combinations during the timeframe measured.
* **Question:** Can this detect other Structural Variants (SVs) besides translocations?
  * **Answer (Nechama):** Yes. By analyzing "loss of signal" or read depth across targets, they can infer Copy Number Variations (CNVs), such as large deletions or duplications.

---

## 3. Comprehensive Summary

**Motivation & Central Argument:**
The central premise of the talk is that **bulk sequencing is insufficient for validating clinical-grade CRISPR therapies.** While bulk methods provide average editing efficiencies, they fail to characterize the heterogeneity of engineered cell populations. The speakers argue that to ensure safety and efficacy, researchers must resolve data at the **single-cell level** to link specific genotypes (on-target efficacy and off-target toxicity) with phenotypes (protein expression).

**Methodology:**
The presentation validated a workflow integrating IDT’s *UncoverSeq* (off-target nomination) and *rhAmpSeq* (confirmation) with Mission Bio’s *Tapestry* platform (single-cell deep confirmation). The case study used CRISPR-Cas9 to edit human T-cells at three loci (*TCRB, TCRA, PDCD1*), benchmarking single-cell findings against standard bulk sequencing.

**Key Findings:**

1. **Precision:** Single-cell analysis accurately quantified the "Target Population" (biallelic knockouts) at ~13%, a metric impossible to derive from bulk averages.
2. **Safety:** It identified that 2% of the therapeutically successful cells harbored unintended off-target mutations, a critical safety insight.
3. **Dynamics:** Time-course data revealed the kinetics of editing and the negative selection of cells with chromosomal translocations over time.
4. **Verification:** The study proved that biallelic frameshift mutations directly correlate with the loss of protein expression (phenotype) in individual cells.

**Limitations & Alternative Perspectives:**

* **Cost:** As noted in the Q&A, single-cell sequencing is significantly more expensive than bulk methods, making it less suitable for early-stage screening.
* **Primer Sensitivity:** The *PDCD1* discrepancy highlighted a technical limitation: targeted amplicon sequencing (both bulk and single-cell) is highly sensitive to primer design. Large deletions can cause "dropouts" leading to false negatives if primers are not carefully positioned.

**Conclusion & Next Steps:**
The speakers conclude that single-cell multi-omics should be the standard for "Deep Confirmation" in therapeutic development. It provides the necessary resolution to define the drug product (the cells) accurately. Potential next steps include implementing the newly announced combined DNA/RNA profiling to see how edits affect global gene expression and using translocation kinetic data to determine the optimal day for harvesting cells to minimize genotoxicity.