# E Coli. Metabolic Engineering with Novel Cofactor NMN

#seminar 

> Systems biology lab meeting at VU

This document provides a detailed summary and analysis of the presentation on engineering microbial metabolism for biotechnological applications.

## Logical Flow of the Presentation

The presentation is structured into the following sections:

1. **Introduction:** Outlines the consortium's goal of maximizing product yields in microorganisms.
2. **Problem & Work Package:** Describes the speaker's specific role, focusing on developing measurement techniques for engineered strains.
3. **Methods Development:** Details two methods for measuring NAD(H) levels: an enzymatic cycling assay and LC-MS.
4. **Results:** Presents validation data for the assays and initial findings from experiments on engineered and wild-type strains under different conditions.
5. **Future Work:** Discusses the next steps, including proteomics and adapting the assay for NADP(H).
6. **Q&A Session:** Addresses questions from the audience.

---

## Section-by-Section Analysis

### 1. Introduction

* **Challenge:** In standard microbial metabolism (like *E. coli*), the substrate (e.g., glucose) is converted not only to the desired product (e.g., lactate) but also to byproducts (formate, acetate, ethanol) and biomass. This distribution of electrons prevents achieving the maximum theoretical yield. The central cofactors NAD and NADH are involved in hundreds of reactions, making targeted changes difficult.
* **Method:** The consortium's strategy is to introduce a "non-canonical" or orthogonal redox cofactor, **nicotinamide mononucleotide (NMN)**. By engineering key enzymes to exclusively use NMN instead of NAD, they can create a separate metabolic pathway that channels all electrons from the substrate to the desired product, thus forcing the cell to make the product to regenerate the NMN cofactor.
* **Transition to Next Section:** This engineering effort requires a way to measure the impact on the cell's metabolism, specifically the levels of these crucial cofactors.

### 2. Problem & Work Package

* **Challenge:** The complete engineered strains are not yet finished. The immediate task is to develop reliable methods to measure NAD and NMN levels to assess the impact of the engineering efforts once they are ready.
* **Methods:** The speaker's primary focus has been on setting up and validating analytical methods to quantify cofactor pools. Key research questions include: What happens to cell growth, fitness, and the native NAD pools when the NAD biosynthesis pathway is altered?
* **Results:** The speaker, with the help of bachelor students, established growth characterization protocols and focused on an enzymatic assay to measure NAD and NADH.
* **Transition to Next Section:** This leads to a detailed description of the measurement methods developed.

### 3. Methods Development

This section details two distinct methods to measure cofactor levels.

* **Method 1: Enzymatic Cycling Assay**
  * **Challenge Resolved:** Provides a cheap, fast, and accessible way to measure NAD and NADH concentrations without requiring expensive equipment like an LC-MS. It also incorporates a quenching step to stop metabolism instantly, which is critical for accurately measuring the rapidly changing NAD/NADH ratio.
  * **Method Used:** The sample is split. NAD is degraded in one half (alkaline conditions), and NADH in the other (acidic conditions). A cycling reaction involving alcohol dehydrogenase then produces a colored compound (reduced INT) at a rate linearly proportional to the NAD or NADH concentration, which is measured with a spectrophotometer.
  * **Results/Output:** The assay successfully measures NAD and NADH levels. However, it has a lower detection limit and, crucially, **cannot measure NMN**.

* **Method 2: LC-MS (Liquid Chromatography-Mass Spectrometry)**
  * **Challenge Resolved:** This method allows for the detection of a much wider range of metabolites simultaneously, including the target non-canonical cofactor **NMN**, as well as NAD, NADP, and ATP. It serves as a validation tool for the enzymatic assay.
  * **Method Used:** A collaboration was set up to use existing LC-MS facilities. A key challenge was adapting the sample preparation, as standard *E. coli* quenching methods can cause the cells to leak metabolites. A yeast quenching protocol using cold methanol was successfully adapted.
  * **Results/Output:** The method is semi-quantitative, meaning it can show relative changes between samples but not absolute concentrations.

### 4. Results

* **Assay Validation:** The enzymatic assay was compared against the LC-MS method using an engineered strain with elevated NAD levels. Both methods showed a consistent increase in NAD, validating the results of the enzymatic assay.
* **Key Finding 1: Growth Rate vs. NAD Pool Size:** An engineered strain with nearly double the normal NAD pool size exhibited a very similar growth rate to the parent strain.
  * **Biological Significance:** This result is surprising because the total NAD pool is generally considered to be a tightly regulated "conserved moiety" essential for metabolic stability. The finding that a cell can tolerate a near-doubling of this pool with little effect on its growth rate challenges this view. It suggests that cellular metabolism is more flexible and robust to fluctuations in the absolute size of this central cofactor pool than previously appreciated.
* **Key Finding 2: Effect of Carbon Source:**
  * Increasing glucose concentration from 10mM to 20mM caused a significant shift in the NAD/NADH ratio and a **doubling of the total NAD+NADH pool**.
    * **Biological Significance:** This is a striking observation. While high glucose is known to cause "overflow metabolism" and shift the *ratio* of NAD+/NADH, a doubling of the *total pool size* is a dramatic and energetically expensive response. It suggests that the cell is not just trying to rebalance the ratio of existing cofactors but is actively synthesizing more NAD molecules to handle the immense redox stress from rapid glucose consumption. This points to an active regulatory mechanism that dynamically manages the total size of the NAD pool in response to nutrient flux, a phenomenon that is not fully understood.
  * Supplementing the media with amino acids to increase the growth rate did not lead to an expected increase in the NAD pool.
* **Transition to Next Section:** With validated methods and intriguing initial data, the speaker outlines the next steps to build on these findings.

### 5. Future Work

* **Proteomics:** The speaker plans to run proteomics experiments to investigate the correlation between the measured cofactor pools (NAD, NADH) and the expression levels of enzymes that use them.
* **Assay Adaptation:** The enzymatic cycling assay will be adapted to also measure NADP and NADPH, which should be achievable with relatively simple changes to the enzyme and substrate used.
* **Inter-lab Comparison:** The developed methods will be used in a larger comparison across different labs within the consortium.

### 6. Q&A Session

* **Question:** Can the enzymatic assay be used to measure NMN?
* **Answer:** No. The assay's specificity comes from the enzyme used. There is currently no known enzyme that is *only* specific to NMN without also reacting with NAD or NADP. The goal of the consortium is to engineer such an enzyme (a specific GAP-DH), but it is not yet available. Other methods like direct light absorbance are not sensitive enough for the low concentrations inside the cell.

---

## Comprehensive Summary

* **Motivation:** The central motivation of the research is to overcome the natural limitations of microbial metabolism for industrial biotechnology. The goal is to maximize the conversion of a substrate into a single, high-value product by preventing the cell from wasting resources on byproducts and excess biomass.

* **Research Question/Central Argument:** The project's central hypothesis is that by creating an orthogonal, self-contained metabolic pathway using a non-native cofactor (NMN), they can force an organism like *E. coli* to produce a desired chemical with maximum efficiency. The speaker's specific research question was how to develop and apply analytical methods to measure these cofactors (both native and non-native) and to use these methods to understand the physiological impact of such radical metabolic engineering on the cell's fitness and internal state.

* **Conclusion:** The presenter successfully developed and validated a low-cost enzymatic assay against a more comprehensive (but semi-quantitative) LC-MS method for measuring NAD/NADH levels in *E. coli*. The initial scientific findings are significant, challenging the conventional view of the NAD pool as a rigidly maintained quantity. The results show that *E. coli* can tolerate a near-doubling of its NAD pool with little impact on growth rate, and that the total pool size can change dramatically depending on environmental conditions (e.g., glucose availability).

* **Potential Next Steps:** The immediate next steps are to use the developed methods to explore the link between cofactor levels and protein expression (proteomics) and to expand the analytical toolkit to include NADP/NADPH. The ultimate goal is to apply these techniques to the fully engineered, NMN-dependent strains to directly test the central hypothesis of the consortium.

