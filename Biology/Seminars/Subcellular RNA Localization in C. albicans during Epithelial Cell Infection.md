# Subcellular RNA Localization in C. albicans during Epithelial Cell Infection

#seminar #candida

> Roan Arends, Evelina Tutucci's lab

## Contextual Knowledge for Understanding the Research

To fully appreciate the findings presented in this talk, several key concepts in microbiology and cell biology are essential:

1. **Candida albicans & Hyphal Morphogenesis:** *C. albicans* is a polymorphic fungus. Its ability to transition from a commensal yeast form to a filamentous hyphal form is central to its virulence. Hyphae are elongated tubes that grow exclusively at the tip (apical growth), allowing the fungus to penetrate host tissues and enter the bloodstream.
2. **Candidalysin (*ECE1*):** A critical discovery in fungal pathogenesis. *ECE1* (Extent of Cell Elongation 1) was long known as a hyphal-specific gene, but it was recently discovered to encode **Candidalysin**, the first peptide toxin identified in a human fungal pathogen. This toxin is secreted into a "protected" invasion pocket between the hyphal tip and the host cell membrane, where it acts as a pore-forming toxin to damage host cells.
3. **Single Molecule Fluorescence In Situ Hybridization (smFISH):** A powerful imaging technique used to detect and localize individual mRNA molecules within fixed cells. By using multiple fluorescently labeled oligonucleotide probes that hybridize to a specific mRNA sequence, each mRNA appears as a distinct diffraction-limited spot under a microscope.
4. **The She3-Myo4 Transport System:** In fungi, specifically the model yeast *Saccharomyces cerevisiae*, mRNA transport is mediated by a complex consisting of an RNA-binding protein (She2), an adapter (She3), and a molecular motor (Myo4). In *C. albicans*, the system is simplified; it lacks a She2 ortholog, and She3 directly binds to both the mRNA and the Myo4 motor to transport "zipcoded" mRNAs along the actin cytoskeleton to the hyphal tip.
5. **c-Fos as a Stress Marker:** *c-Fos* is an "immediate-early" gene in mammalian cells. Its expression is rapidly induced in response to various stimuli, including membrane damage and stress signaling. In this research, it serves as a readout for the epithelial cell's response to Candidalysin-induced damage.

---

## Sectional Report: Subcellular RNA Localization in *C. albicans*

### 1. Introduction: The Clinical and Biological Problem

**Challenges & Motivation:** The speaker highlights the high mortality rate (~50%) of invasive candidiasis in immunocompromised patients and the rising global threat of antifungal resistance. The central challenge is understanding the "efficiency" of *C. albicans* as a pathogen.
**Logical Flow:** The talk establishes that the "morphological switch" from yeast to hyphae is the primary virulence factor. Because hyphae grow directionally at the tip, the cell faces a logistical challenge: how to move the necessary "building blocks" (proteins and membranes) from the nucleus to the distant growth site.
**Methods:** The speaker draws parallels to other kingdoms (neurons, *E. coli*), noting that transporting mRNA for local translation is more efficient than transporting individual proteins.

### 2. Methodology: Dual-Organism smFISH

**Challenges Resolved:** Traditional infection models are population-based studies that obscure cell-to-cell variability. The speaker aims to resolve this by developing a dual-organism smFISH method.
**Methods Used:**

* **Probes:** Specifically designed to account for both the *C. albicans* and the human epithelial (gingival) genomes to avoid cross-reactivity.
* **Model:** Gingival cells are grown to congruency to form a biological barrier. Infection is initiated with a controlled ratio (1 hypha per 10 epithelial cells).
* **Fixation/Hybridization:** Cells are fixed after 6 hours of infection to capture the spatial orientation of mRNAs in both organisms.
**Results:** The lab previously identified *ECE1* and *HWP1* (cell wall protein) as mRNAs that actively localize to the hyphal tip. This localization ensures high local concentrations of Candidalysin (*ECE1*) at the point of invasion.

### 3. Host Response Mapping: c-Fos Induction

**Challenges Resolved:** Measuring the "physiological concentration" of damage at the single-cell level.
**Methods & Results:**

* The method was validated using serum deprivation to confirm that *c-Fos* induction could be quantified.
* **Spatial Heatmaps:** By mapping *c-Fos* expression intensity, the researchers observed a "fractal" pattern. Host cells showed high stress only if they were directly in the path of or invaded by a hypha.
* **Knockout Validation:** Using an *ece1Δ* (Candidalysin-deficient) mutant, they confirmed that without this toxin, the host *c-Fos* response is abolished, even if invasion occurs.
**Transition:** This led to a deeper mechanistic question: Is the *localization* of the mRNA (and not just the presence of the protein) essential for virulence?

## 4. Mechanism: The She3 Transport Pathway

**Methods Used:** The researchers utilized *she3Δ* (transporter knockout) and *SHE3* rescue strains to investigate the transport of *ECE1* and *HWP1*.
**Results:**

* In wild-type (WT) cells, *ECE1* is tightly localized at the tip.
* In *she3Δ* mutants, the mRNA is dispersed throughout the hyphal compartment, though it is still present.
* In she3 partial rescues, the ECE1 localization is partially restored.
* **Intensity/Distance Quantification:** By segmenting hyphae from tip to nucleus, they mathematically demonstrated the loss of the localization gradient in the mutant.
* **Virulence Impact:** Crucially, the *she3Δ* strain—despite still having the *ECE1* gene—showed a host *c-Fos* response nearly as low as uninfected controls. This suggests that without mRNA localization to the tip, the local concentration of Candidalysin is insufficient to trigger host damage.

---

## Comprehensive Summary

### Motivation and Central Argument

The research is motivated by the need to understand how *C. albicans* efficiently invades host tissue. The central argument is that **subcellular mRNA localization** is a critical, yet understudied, component of fungal virulence. Specifically, the fungus does not just need to produce the toxin Candidalysin; it must transport the *ECE1* mRNA to the hyphal tip to ensure the toxin is translated and secreted exactly where it can damage the host membrane (the "invasion pocket").

### Conclusion

The study successfully established a dual-organism single-cell imaging model. The key findings are:

1. Host cell stress (measured by *c-Fos*) is spatially restricted to the immediate site of hyphal contact.
2. The She3-Myo4 transport system is required to localize *ECE1* and *HWP1* mRNAs to the hyphal tip.
3. Disrupting this localization (via *she3Δ*) significantly attenuates the host's stress response, demonstrating that the spatial organization of the transcriptome is a prerequisite for effective infection.

### Current Limitations and Alternative Perspectives

* **Pleiotropic Effects:** The *she3Δ* mutant disrupts the transport of many mRNAs, not just *ECE1*. The observed reduction in virulence might be a compounded effect of missing multiple localized factors at the tip.
* **Marker Specificity:** The speaker acknowledges that *c-Fos* is a broad stress marker. It may not distinguish between different types of host cell damage or signaling.
* **In Vitro Model:** While gingival cells are relevant, the complexity of a 3D tissue or a whole-organ infection (involving immune recruitment) is not yet captured.

### Potential Next Steps

1. **Motif Discovery:** Identifying the "zipcodes" (specific RNA sequences) that She3 binds to within *ECE1* and *HWP1*.
2. **Zipcode Knockouts:** Creating mRNA-specific localization mutants (e.g., an *ECE1* gene that produces mRNA that cannot be transported) to isolate the effect of localization from the transporter's global role.
3. **Expanded Host Markers:** Integrating additional fluorescent markers to better characterize the epithelial response beyond general stress.
