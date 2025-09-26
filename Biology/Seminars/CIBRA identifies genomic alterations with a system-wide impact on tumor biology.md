# CIBRA identifies genomic alterations with a system-wide impact on tumor biology

#paper 
[link](https://academic.oup.com/bioinformatics/article/40/Supplement_2/ii37/7749081)

## 1. Motivation

Cancer is driven by genomic instability, which produces numerous somatic alterations—from single nucleotide variants (SNVs) to large-scale structural variants (SVs) and somatic copy number aberrations (SCNAs). Yet, only a subset of these alterations truly impact tumor biology by triggering broad, system-wide changes in gene expression. Conventional approaches (frequency‐based or impact prediction methods) either require very large cohorts or are limited to specific variant types (e.g. missense SNVs). Hence, there is an unmet need for a method that can prioritize those alterations that elicit a significant systemic response—especially for low-frequency events and structural variants that are often overlooked.

**CIBRA** (Computational Identification of Biologically Relevant Alterations) is proposed with the motivation to use transcriptomics as a phenotypic readout in order to measure the system-wide impact of each genomic alteration. In doing so, CIBRA can help refine the definition of cancer-driving events and better prioritize biomarkers for diagnostics, disease progression, and treatment response.

---

## 2. Research Question

The paper answers the question:  
**How can one systematically determine the system-wide impact of genomic alterations by integrating genomics with transcriptomics data?**  

Specifically, it aims to identify which somatic alterations (whether SNVs, SCNAs, or SVs) induce a measurable, widespread change in downstream gene expression—thereby flagging alterations that are most likely to drive tumor biology.

---

## 3. Relevant Background Information

### Genomic Instability and Somatic Alterations

- **Cancer Genomics:**  
  Tumors accumulate many somatic alterations; however, only a fraction of these are functionally relevant (i.e., oncogenic drivers or tumor suppressor hits). Most frequency-based detection methods work best on large cohorts and tend to miss low-frequency events.
- **Limitations of Existing Methods:**  
  Frequency-based methods (e.g., MutSigCV) and impact prediction tools (e.g., SIFT, PolyPhen) have limitations—they either require high-frequency events or only address missense variants within coding regions, respectively.

### Transcriptome as a System-Wide Readout

- **Expression Data as Phenotype:**  
  The transcriptome represents the cellular state and reflects the consequences of genomic alterations. Prior work has shown that the gene expression profile can capture system changes such as genomic instability.
- **Data Types and Acquisition:**  
  - **Genomics Data:** Whole Exome Sequencing (WES) data from The Cancer Genome Atlas (TCGA) covering 33 cancer types, and whole genome sequencing (WGS) data from the Hartwig Medical Foundation for metastatic colorectal, breast, and lung cancers. In these datasets, “silent” or non-impactful variants are filtered out.
  - **Transcriptomics Data:** RNA sequencing (RNA-seq) data from the same cohorts is used to measure gene expression across samples. By comparing expression in samples with versus without a given genomic alteration (cases vs. controls), the system-wide impact can be assessed.

---

## 4. Relevant Theories

Several interrelated theories form the conceptual basis for CIBRA:

- **System-Wide Impact Theory:**  
  The fundamental idea is that biologically impactful genomic alterations induce broad changes in the transcriptome. Thus, if a gene is truly a driver, its alteration will result in a characteristic systemic transcriptional response.
  
- **Beta-Uniform Mixture Modeling:**  
  By performing differential expression analysis between altered (case) and unaltered (control) samples, one obtains a distribution of p‐values. This distribution is expected to be a mixture: a uniform component representing non–differentially expressed genes and a beta-distributed component for genes altered due to the mutation. The integration between these components (termed the “significant area”) quantifies the magnitude of the system-wide effect.
  
- **Evolutionary Dynamics of Cancer:**  
  Underlying frequency-based methods is the Darwinian evolution model of tumorigenesis (variation and selection). However, instead of solely relying on mutation recurrence, CIBRA posits that the functional impact on the cellular system (as measured by transcriptomic changes) is a more direct indicator of a mutation’s biological significance.

---

## 5. Methods

### Overview of the CIBRA Pipeline
CIBRA integrates genomics and transcriptomics through the following steps:

1. **Data Input and Group Definition:**  
   - Samples are grouped into “cases” (those with a given genomic alteration) and “controls” (those without it). This is done separately for different types of alterations (e.g., coding SNVs, SCNAs, SVs).

2. **Differential Expression Analysis:**  
   - RNA-seq data are compared between cases and controls to obtain a genome-wide P‐value distribution reflecting differences in gene expression.
  
3. **Beta-Uniform Mixture Model Fitting:**  
   - The P‐value distribution from the differential expression is modeled as a mixture of a Beta distribution (representing the alternative hypothesis—significant, nonrandom changes) and a Uniform distribution (null hypothesis).  
   - The model yields shape parameters (typically denoted as λ and α) and allows calculation of the “significant area”—the integral where the Beta component exceeds the Uniform component. This area represents the **CIBRA impact score**.

4. **Permutation Testing:**  
   - The statistical significance of the impact score is assessed using 1000 sample permutations, comparing the observed impact to a null distribution.

5. **Refinement by Mutation Category and Genomic Region:**  
   - The method can dissect the overall impact by evaluating distinct mutation types (e.g., missense variants vs. nonsense variants, splice variants) or combinations (e.g., SNVs together with copy-number loss for tumor suppressor genes), and even zooming into specific subregions of a gene (e.g., codon-specific effects in KRAS).

6. **Similarity Score:**  
   - An additional similarity score is derived to compare the system-wide transcriptomic impact between different genomic alterations—either variations within the same gene or between different genes.

7. **Machine Learning Comparison:**  
   - As an alternative approach, the authors trained a random forest classifier to predict genomic alteration status from gene expression profiles. Although effective, this ML approach requires sufficiently large case–control sets (≥50 each) and is less applicable when sample numbers are small; CIBRA is effective with as few as 10 cases/controls.

---

## 6. Results

### Pan-Cancer Screening with TCGA Data
- **Coding SNVs in Primary Cancers:**  
  In a genome-wide screen for 33 cancer types, 8.9% of genes with coding SNVs showed a significant system-wide impact (adjusted P ≤ 0.01). Notably, 54.3% of these were known cancer driver genes (registered in the COSMIC cancer gene census). The method achieved an ROC-AUC of 0.79 in identifying established cancer genes, outperforming other driver detection methods that use genomics data alone.

### Assessment of Structural Variants (SVs) and SCNAs
- **Metastatic Cancers:**  
  Analysis of metastatic colorectal, breast, and lung cancers from the Hartwig Medical Foundation revealed that 16.5% of genes affected by any alteration (SNVs, SCNAs, or SVs) exhibited a significant system-wide impact.  
  - Strikingly, 30.3% of genes affected by SVs showed a significant impact. This suggests that the role of SVs in altering tumor biology may have been under-reported by frequency-based methods.
  
### Impact Refinement by Mutation Type and Genomic Location
- **Example – BRAF and KRAS:**  
  In BRAF, while the overall signal was not significant, restricting the analysis to missense variants (e.g. the oncogenic V600E mutation) produced a significant impact score. Similarly, KRAS codon 12 variants exhibited a distinct, high impact compared to KRAS codon 13 variants in metastatic colorectal cancer.
  
- **Tumor Suppressor Genes:**  
  For tumor suppressors such as APC and TP53, combining coding SNVs with SCNA (copy-number loss) resulted in a higher impact score—reflecting the "two-hit" hypothesis.
  
### Similarity of Expression Effects
- **Comparing Impact Between Variants:**  
  The similarity score allowed the authors to compare the gene expression effects between different mutations. For example, KRAS codon 12 and BRAF V600 had significant similarity and anti-similarity patterns, reflecting differences in their downstream signaling impacts even though both are parts of the EGFR pathway.

### Machine Learning vs. CIBRA Impact Score
- The ML model (random forest) could predict mutation status based on transcriptomic data with high ROC-AUC scores for some cancer genes; however, it required larger sample sizes. CIBRA, by contrast, was applicable with as few as 10 cases and controls and successfully identified that genes like TTN (often heavily mutated due to its size) lack a system-wide impact in colorectal cancer.

---

## 7. Validations

- **Internal Validation and Permutation Testing:**  
  The significance of each CIBRA impact score was validated using 1000 permutation tests to ensure that observed system-wide changes were unlikely to have arisen by chance.
  
- **Benchmarking Against Known Drivers:**  
  The method’s ability to identify known tumor suppressor genes and oncogenes was benchmarked against the COSMIC cancer gene census, resulting in a robust ROC-AUC of 0.79.
  
- **Impact Refinement Consistency:**  
  CIBRA’s ability to refine impact by mutation type and genomic location (e.g., KRAS codon-specific effects) was consistent with established clinical and biological findings.
  
- **Comparison with Machine Learning Approaches:**  
  The consistent performance of CIBRA, especially with small sample sizes, further validated its utility versus a machine learning–based approach that requires larger datasets.

---

## 8. Implications

- **Enhanced Driver Identification:**  
  CIBRA provides an innovative way to prioritize genomic alterations that truly impact tumor biology by capturing system-wide changes. This can refine the list of potential cancer drivers beyond what frequency-based methods can achieve.
  
- **Uncovering Under-Reported Alterations:**  
  The striking finding that many structural variants show a substantial system-wide impact implies that SVs may play a larger role in cancer development and progression than previously appreciated.
  
- **Improved Biomarkers for Diagnostics and Treatment:**  
  By linking genomic alterations to widespread transcriptomic changes, CIBRA can help in the development of more nuanced biomarkers. These refined biomarkers could improve diagnostic accuracy, prognostic assessments, and the personalization of treatment strategies.
  
- **Broad Applicability:**  
  Because the method only needs a small number of cases and controls, it can be applied even to rare alterations or small clinical cohorts.

---

## 9. Clinical Problem Addressed

One of the central challenges in oncology is to distinguish driver alterations from passenger mutations, particularly when patient samples are limited and many alterations are low-frequency or involve complex structural rearrangements. CIBRA addresses this clinical problem by:

- **Prioritizing Clinically Relevant Alterations:**  
  By integrating genomics and transcriptomics, it highlights those alterations that create a significant, system-wide change in tumor biology. This shows which mutations are likely to contribute to tumor progression or affect treatment outcomes.
  
- **Informing Personalized Cancer Care:**  
  With refined biomarkers that capture the impact of genomic alterations, CIBRA can help guide treatment decisions—be it in selecting targeted therapies or in designing follow-up experiments to validate potential clinical interventions.
  
- **Potential Utility in Therapeutic Stratification:**  
  Ultimately, CIBRA’s approach may allow clinicians to preselect patients for certain therapies based not only on mutation presence but on the functional consequences of these mutations across the cellular system.

---

## In Summary

The paper introduces CIBRA, a novel integrative method that quantifies the system-wide impact of genomic alterations by combining genomics (from WES/WGS data) with transcriptomics (RNA-seq) using a Beta–Uniform mixture model framework. The method produces a CIBRA impact score that reflects the extent of transcriptomic changes associated with a given alteration. Through pan-cancer analyses and studies in metastatic cancers, CIBRA successfully identifies known oncogenes and tumor suppressor genes, reveals that many structural variants have a significant system-wide effect, and refines impact based on mutation type and genomic location. Validated through permutation tests, ROC analyses, and comparisons with machine learning models, CIBRA has significant implications for prioritizing potential drivers in cancer and improving biomarker development—thereby addressing challenges in personalized cancer diagnostics and treatment strategies.