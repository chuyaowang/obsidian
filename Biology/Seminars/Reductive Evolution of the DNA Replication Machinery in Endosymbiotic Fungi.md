# Reductive evolution of the DNA replication machinery in endosymbiotic fungi

#paper 
2025, bioRxiv

## Abstract-Level Overview (Expanded)

This paper investigates **why some fungal lineages that live as obligate endosymbionts**—specifically **Glomeromycotina** (arbuscular mycorrhizal fungi) and **Microsporidia** (intracellular parasites)—have **lost major DNA polymerase complexes** that are normally essential for accurate DNA replication and repair. Surprisingly, these fungi survive despite losing enzymes required for:

* **Replication** (e.g., Polε, the canonical leading-strand polymerase)
* **Translesion synthesis (TLS)** (e.g., Polζ, Rev1, Polη), which allow replication across damaged DNA

These gene losses correlate with:

* **Higher genetic variation and SNP rates**
* **Loss of accessory subunits of the polymerase holoenzymes**
* **A remodeled or minimal replisome (“replisome reduction”)**

The paper’s striking biological insight is that **Rhizophagus irregularis**, a model AM fungus, **only activates its cell cycle and DNA replication when in symbiosis with a plant host**, suggesting **host-dependent regulation of fungal DNA replication**.

Ultimately, the authors propose that reduced replication machinery creates:

* **Alternative replication strategies**
* **Higher mutation rates**
* **Novel routes for adaptation**
* **Strong evolutionary coupling between hosts and endosymbionts**

---

## Introduction (Background-heavy)

### 1. Plant–fungal symbiosis and the groups studied

Plants and fungi frequently form long-term **mutualistic symbioses**.
A prominent example is **arbuscular mycorrhizal (AM) symbiosis**, in which fungi in the subphylum **Glomeromycotina** colonize plant roots and exchange nutrients.

Other relevant fungal groups include:

* **Mucoromycotina** – related fungi that include mutualists and decomposers.
* **Microsporidia** – obligate intracellular parasites of animals.
* **Cryptomycota** – early-diverging relatives of Microsporidia, parasites of algae and other protists.

---

### 2. Obligatory biotrophy and metabolic dependency

Many AM fungi exhibit **obligate biotrophy**, meaning they **cannot grow without a host**.
A defining feature: **loss of autonomous fatty acid biosynthesis**, making them dependent on the plant for lipids.

---

### 3. Evolutionary context: how organisms become obligate endosymbionts

A typical evolutionary trajectory:

1. **Genome expansion** (acquisition of mobile elements)
2. **Genome reduction** (loss of genes not essential for intracellular life)
3. **Loss of pathways including DNA repair and replication factors**

In many prokaryotic endosymbionts, loss of replication/repair pathways increases mutation rates, which:

* Causes genome instability
* Can, paradoxically, promote **faster adaptation**

The authors suggest a similar trajectory may occur in fungal endosymbionts.

---

### 4. The study’s central motivation

The authors ask:

> **How complete is the DNA replication machinery in fungal endosymbionts, and how do they replicate their DNA if they have lost essential polymerases?**

They investigate:

* **Lineage-specific DNA polymerase losses**
* **Impact on mutation rates**
* **Co-loss of holoenzyme subunits (replisome reduction)**
* **Functional consequences for cell cycle activity**

---

### Key Theory: “Replisome reduction”

The **replisome** is the large protein complex that performs DNA replication.
The paper proposes that in some fungi:

* The replisome has **lost multiple essential components**,
* Leading to **lineage-specific shifts in mutation rate** and
* **Alternative replication strategies** required for survival.

This parallels the reductive evolution known in bacterial endosymbionts.

---

## Results

---

### 1. Loss of DNA polymerase genes in eukaryotic intracellular parasites and mutualists

#### Main Questions

* Which DNA polymerases are present or absent across fungal lineages?
* Are losses correlated with lifestyle (symbiotic vs. free-living)?

#### Methods Used

* Phylogenomics (using genomes of 69 fungal species and outgroups)
* Homology inference using DIAMOND, PSI-BLAST, TBLASTN
* Structural homology via AlphaFold3 + FoldSeek
* BUSCO completeness checks

#### Key Findings

* Multiple **B-family and Y-family polymerases** involved in TLS and replication were lost in:

  * **Glomeromycotina**
  * **Microsporidia**
* Losses include **Polζ, Polη, Polε, Rev1**, depending on lineage.
* These losses were **true gene losses**, not artifacts.
* Microsporidia also lost **A-family polymerases** due to their loss of mitochondria.

#### Conclusion

These fungi independently lost core replicative and repair polymerases, particularly those for:

* **Leading-strand synthesis (Polε)**
* **Translesion synthesis (Polζ, Rev1, Polη)**

Such losses are rare in eukaryotes and suggest a **fundamental reshaping of their replication strategies**.

---

### 2. Lineage-specific sequential loss of polymerases

#### Main Questions

* Did different lineages lose polymerases in similar or parallel sequences?
* Are accessory subunits also lost?

#### Key Findings

* In **Glomeromycotina**, the sequence of catalytic subunit losses matches the phylogeny:

  1. Rev1 lost in early ancestor
  2. Polζ lost next
  3. Polη lost later
  4. Polε lost last (in the Glomeraceae family)

* In **Microsporidia**, the order is different but still sequential:

  1. Polζ lost first
  2. Then Rev1
  3. Then Polη
  4. Other losses follow during mitochondrial reduction

* **Accessory subunits** such as Rev7 (Polζ) and Dpb2 (Polε) were lost **concomitantly** with their catalytic partners → strong physical/functional coupling.

* Glomeraceae also lost **Ctf18-RFC clamp loader components** (Ctf18, Ctf8, Dcc1) that normally work with Polε.

#### Conclusion

Both lineages show **parallel reductive evolution** in DNA replication machinery, including both catalytic and accessory proteins—a hallmark of structural dependency.

---

### 3. Cell cycle activity in *R. irregularis*: active with host, suppressed without host

#### Main Question

Does *R. irregularis*, which lacks Polε, replicate DNA autonomously?

#### Methods

* Germination of fungal spores **with and without plant hosts**
* **qPCR** quantification of DNA content
* **RNA-seq** expression profiling
* **Confocal microscopy** to identify mitotic nuclei

#### Key Results

* Spores germinating **without a host**:

  * No increase in chromosomal DNA over 21 days
  * Low expression of replication and repair genes
  * Nuclei appear stuck in **G1 phase**

* In **symbiosis with plant**:

  * Strong upregulation of replication genes
  * Evidence of mitotic chromosomal segregation
  * High occurrence of paired nuclei (anaphase/telophase stages)
  * Suggests the cell cycle is **host-triggered**

#### Conclusion

*R. irregularis* appears unable to progress through S-phase without host-derived signals/metabolites.
This implies a **deep functional integration** between plant and fungal cell cycles.

---

## Quantitative Summary

| Topic                  | Key Quantitative Findings                                                                |
| ---------------------- | ---------------------------------------------------------------------------------------- |
| Polymerase Loss        | Glomeraceae missing 4/9 standard eukaryotic polymerases                                  |
| Mutation Levels        | Polη⁻ Polε⁻ species show **higher SNP rates** and lower WGA alignment                    |
| DNA Replication (qPCR) | No chromosomal DNA increase over 21 days host-free                                       |
| Gene Expression        | Replication genes strongly upregulated in planta (RNA-seq)                               |
| Nuclear States         | Higher % of paired nuclei in planta vs in vitro (exact values visually shown in Fig. 5e) |

---

## Data Types and Acquisition

* **Genomes**: NCBI assemblies; assessed using BUSCO.
* **Protein sequences**: DIAMOND/PSI-BLAST/TBLASTN homology.
* **RNA-seq**: public datasets (STAR + featureCounts + DESeq2).
* **Microscopy**: confocal and fluorescence imaging.
* **qPCR**: chromosome copy number quantification.

---

## Figures and Tables — Key Contributions

### Figure 1

Phylogenetic presence/absence of polymerases across fungi and other eukaryotes → demonstrates widespread but lineage-specific losses.

### Figure 2

Fine-scale mapping of sequential polymerase losses in Glomeromycotina.

### Figure 3

Loss of Polε-associated replisome factors → visual model of a remodeled fungal replisome.

### Figure 4

Quantitative link between polymerase loss and increased SNP rates.

### Figure 5

Cell cycle activation only in symbiosis → microscopy & qPCR.

---

## Methods (Explained Simply)

While not algorithmic in a rigid sense, the core bioinformatics pipeline follows:

### Polymerase Identification Pipeline

1. **Collect proteomes and genomes**
2. **Search for homologs** using:

   * DIAMOND (fast homology)
   * PSI-BLAST (iterative refinement)
   * TBLASTN (genome-level search)
3. **Structural homology validation** using:

   * AlphaFold3 protein prediction
   * FoldSeek structure-comparison
4. **Phylogenetic reconstruction** with IQ-TREE or FastTree
5. **Presence/absence matrix construction**

This is essentially a **homology-inference + phylogenomics algorithm**.

---

## Assumptions and Premises

* Genome assemblies are sufficiently complete for reliable inference (validated via BUSCO).
* Homology detection methods are sensitive enough to rule out hidden/diverged genes.
* Structural confirmation using AlphaFold3 avoids false negatives.

These assumptions allow them to infer **true gene loss** rather than annotation failure.

---

## Alternate paths explored

The authors tested whether polymerase absence might be due to:

* Extremely divergent sequences (tested with structural homology)
* Assembly incompleteness (checked via BUSCO correlations)
* Accelerated evolution causing detection failure (checked via bitscore analysis)

All evidence supports **real biological gene loss**.

---

## Discussion — Interpretation and Implications

### Major Insights

1. **Independent reductive evolution** of the DNA replication machinery has occurred in two unrelated endosymbiotic fungal lineages.
2. **Loss of canonical leading-strand polymerase Polε** in Glomeraceae is unprecedented and suggests alternative replication modes (perhaps Polδ takeover).
3. These losses are **correlated with higher mutation loads**, offering **adaptive flexibility**.
4. *R. irregularis* depends on its host to activate its cell cycle, implying **host-controlled fungal replication**.
5. The findings parallel reductive trends in **bacterial endosymbionts**, suggesting convergent evolution across domains.

---

## Limitations

* Genome sampling of Cryptomycota is incomplete → ancestral order of losses remains uncertain.
* Experimental validation of the alternative replisome is indirect; biochemical assays are missing.
* Mutation rates estimated from SNP accumulation may be influenced by population structure, not only polymerase loss.

---

## Implications

* **Evolutionary biology**: Shows extreme plasticity in DNA replication systems in eukaryotes.
* **Symbiosis research**: Reveals deeper plant–fungus integration than previously assumed.
* **Fungal biotechnology**: Suggests that AM fungi may require *in planta* environments for genome editing or replication-dependent processes.
* **Genome evolution**: Highlights mutation-rate modulation as a driver of fungal adaptability and niche expansion.

---

## Conclusion

This paper provides an unexpected and paradigm-shifting view of how fungal endosymbionts operate with highly reduced DNA replication machinery. By linking polymerase loss to increased mutation rates, replisome remodeling, and host-dependent cell-cycle activation, the work opens new conceptual avenues for understanding fungal evolution, symbiosis biology, and the boundaries of essential cellular processes.

