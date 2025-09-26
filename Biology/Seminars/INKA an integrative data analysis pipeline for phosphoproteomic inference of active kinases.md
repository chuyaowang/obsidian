# INKA, an integrative data analysis pipeline for phosphoproteomic inference of active kinases

#paper 
[link](https://www.embopress.org/doi/full/10.15252/msb.20188250)

## 1. Motivation

The study is driven by the clinical need for personalized cancer therapy. Because kinases are major regulators of cell signaling and frequently become hyperactive in tumors, they represent attractive targets for drug intervention. However, given that many cancers display complex kinase signaling patterns, it is a major challenge to pinpoint which kinases are truly driving tumor growth. Mass spectrometry (MS)–based phosphoproteomics can provide global phosphorylation profiles but translating these large, complex datasets into actionable insights requires an analysis pipeline that can robustly infer kinase activity from a single clinical sample. 

In essence, the authors want to overcome the limitations of existing methods that use either a kinase‐centric or a substrate‐centric view alone. Their goal is to integrate both sources of evidence to deliver a robust ranking of active kinases that could guide individualized therapy.

---

## 2. Research Question

The paper asks:  
**How can one integrate multiple lines of phosphoproteomic evidence—both direct (kinase phosphorylation) and indirect (substrate phosphorylation)—to accurately infer and rank active kinases in a single biological sample?**

This question is central because, in a clinical setting, only a limited amount of tumor material may be available, and decisions about targeted therapy must be based on comprehensive signaling information from that one sample.

---

## 3. Relevant Background Information

Several elements shape the background against which this work is set:

- **Role of Kinases in Cancer:**  
  Approximately 75 kinases are known to drive tumorigenesis. Aberrant, hyperactive kinase signaling is a hallmark of cancer and the target of many approved therapies. Yet, even with extensive genomic profiling, only a subset of treated patients benefit, and drug resistance often develops.

- **Mass Spectrometry–Based Phosphoproteomics:**  
  MS-based approaches can capture thousands of phosphorylation events. Earlier studies, like the work by Rikova et al. (2007), used spectral counts (a semi-quantitative measure) of phosphopeptides to rank kinase activity. However, these “kinase‐centric” methods focus only on phosphorylation events within the kinase molecules themselves.

- **Substrate-Centric Approaches:**  
  Alternatively, analyses have focused on substrates—phosphopeptides generated from proteins that are known targets of kinases. Tools such as KSEA and KARP rely on databases like PhosphoSitePlus and predictive algorithms like NetworKIN. However, such methods by themselves might miss important nuances, particularly when kinase–substrate databases are incomplete.

- **Need for Integrated Analysis:**  
  Over time it became clear that neither the kinase-centric nor the substrate-centric approach was fully sufficient on its own. The innovation here lies in integrating both types of evidence within a single framework, enabling a more reliable signature of kinase activity from the phosphoproteomic data obtained from one sample.

---

## 4. Relevant Theories

Several conceptual frameworks underpin the INKA approach:

- **Kinase Activity Inference:**  
  The fundamental idea is that a hyperactive kinase will not only be heavily phosphorylated itself (kinase-centric evidence) but will also phosphorylate many of its substrates (substrate-centric evidence). Both signals are informative of its overall activity in a cell.

> [!info]- Phosphopeptide detection
> Phosphopeptides are short segments of proteins that have been post‐translationally modified by the addition of phosphate groups—typically on serine, threonine, or tyrosine residues. In the context of this study (INKA: an integrative pipeline for phosphoproteomic inference of active kinases), phosphopeptides serve as the primary readout for assessing cellular signaling activity. Here’s a detailed breakdown of what they are and how they are detected:
> 
> ### What Are Phosphopeptides?
> 
> - **Definition and Role:**  
>   Phosphopeptides are the fragments of proteins that remain phosphorylated after the protein is enzymatically digested (commonly with trypsin). These phosphate modifications are key regulators of protein function and signaling. Since kinases add a phosphate group to specific residues, the presence and abundance of phosphopeptides—especially those derived from kinases or their substrates—provide a snapshot of the cellular signaling state.
> 
> - **Relevance in the Study:**  
>   The INKA pipeline leverages quantitative information from phosphopeptides to infer the activity level of kinases in a sample. In essence, the phosphorylation status (captured as phosphopeptides) reflects both direct kinase phosphorylation (kinase-centric evidence) and the phosphorylation of downstream substrates (substrate-centric evidence).
> 
> ### How Are Phosphopeptides Detected?
> 
> 1. **Sample Preparation and Protein Digestion:**  
>    - Proteins isolated from a biological sample (cell lines, biopsies, or xenografts) are first digested, usually using the enzyme trypsin, which cleaves proteins into smaller peptides.
>    - This digestion leaves many peptides phosphorylated if they originally contained phosphate groups.
> 
> 2. **Enrichment of Phosphopeptides:**  
>    - Because phosphorylated peptides are typically less abundant in the complex mixture, specialized enrichment methods are employed to isolate them.  
>    - **Immunoaffinity Enrichment:** For phosphotyrosine peptides, antibodies specific to phosphotyrosine are used to pull down these modified peptides.
>    - **Metal Oxide Affinity Chromatography (MOAC):** Methods such as titanium oxide (TiOx) enrichment are often used to capture phosphoserine and phosphothreonine peptides.
>    - These steps help to “fish out” the phosphopeptides from the bulk of the non-modified peptides, thereby increasing their detectability.
> 
> 3. **Mass Spectrometry Analysis:**  
>    - The enriched phosphopeptides are then injected into a liquid chromatography-tandem mass spectrometry (LC-MS/MS) system.
>    - LC separates the peptides based on their physical and chemical properties, while MS/MS detects and fragments them.
>    - The resulting spectra are analyzed with specialized software (e.g., using a tool like MaxQuant) to identify each peptide and determine which specific residues are phosphorylated, as well as to quantify their abundance.  
>    - This quantitative data (often in the form of spectral counts or intensities) is used to infer the relative levels of phosphorylation across different proteins and peptides.
> 
> ### Summary
> 
> - **What They Are:**  
>   Phosphopeptides are peptides that contain phosphate groups attached to specific amino acid residues. They are indicative of the activity of kinases and represent a direct readout of cellular phosphorylation events.
> 
> - **How They’re Detected:**  
>   The process involves enzymatic digestion of proteins, enrichment of phosphorylated peptides using either antibody-based (for tyrosine phosphorylation) or metal oxide affinity methods (for serine/threonine phosphorylation), and their subsequent identification and quantification via LC-MS/MS.
> 
> In the INKA study, these phosphopeptide measurements are crucial because they provide both the direct and indirect evidence required to assess and rank kinase activity in single samples. This information, in turn, can guide more personalized therapeutic strategies by identifying the hyperactive kinases that may be driving cancer growth.

- **Multipronged Evidence Integration:**  
  The authors build on the theory that integrating different, complementary types of evidence (direct measurements and indirect predictions) leads to higher confidence in the inference process. In INKA, evidence from phosphopeptides mapping to kinases and those mapping to known or predicted substrates is combined using a _geometric mean_, ensuring that both components contribute to the final score.

- **Network-Based and Statistical Approaches:**  
  By incorporating methods such as permutation tests to generate null distributions and calculate p values, the approach uses statistical theory to assess the significance of the inferred activity. The “skew” parameter further emphasizes the relative contribution of kinase- versus substrate-derived data.

---

## 5. Method

The INKA pipeline is a multi-step analysis framework that integrates four lines of evidence:

1. **Kinase-Centric Evidence:**  
   - **Total Phosphopeptides from Kinases (“Kinome”):** All phosphopeptides assigned to a given kinase are summed (often using spectral counts as surrogates for phosphorylation abundance).  
   - **Activation Loop Phosphorylation:** Since phosphorylation in the activation loop is critical for functionality, a separate score is computed for peptides derived from this key region.

2. **Substrate-Centric Evidence:**  
   - **Experimental Kinase–Substrate Data:** Using curated databases like PhosphoSitePlus, the pipeline associates observed phosphopeptides (from substrates) to their kinases.
   - **Predicted Kinase–Substrate Relationships:** The NetworKIN algorithm is employed to assign additional phosphosites to likely producing kinases based on sequence motifs and network information.

3. **Integration of Evidence:**  
   - For each kinase, the two kinase-centric scores are summed, and similarly the two substrate-centric scores are summed. Then, the INKA score is calculated as the geometric mean of these two sums.  
   - A “skew” parameter is computed to indicate whether the overall evidence leans more toward the kinase measurements or toward substrate evidence.

4. **Visualization and Interpretation:**  
   - Results are shown in scatter plots (with the vertical axis being the overall INKA score and the horizontal axis representing the evidence skew), bar graphs of the top-ranked kinases, and network diagrams mapping inferred kinase–substrate relations.
   - Statistical significance (p values) is assessed via a randomization procedure (permutations of peptide–spectral count links and kinase–substrate annotations). 

The entire pipeline can work on label-free data (spectral counts or intensities) and is designed to be used on single samples, which is critical for clinical applications.

---

## 6. Results

The authors applied INKA to multiple settings:

- **Oncogene-Driven Cancer Cell Lines:**  
  Four well-studied cell lines are analyzed:
  - **K562 (CML)**: INKA correctly ranks the fusion kinase BCR–ABL (ABL1) as highly active.
  - **SK-Mel-28 (Melanoma):** While BRAF itself might not be captured via phosphotyrosine (pTyr) approaches, the downstream MEK/ERK pathway (e.g., MAPK3) is detected as hyperactive.
  - **HCC827-ER3 (NSCLC):** The method identifies EGFR and MET as top active kinases in an erlotinib-resistant setting.
  - **H2228 (NSCLC):** For cells harboring an EML4-ALK fusion, INKA ranks ALK and other connected kinases (like SRC and PTK2) highly.

- **Differential Analyses:**  
  In both genetic (wild-type versus mutant) and pharmacologic settings (untreated versus erlotinib-treated cells), INKA scoring captured the expected changes—such as a drop in EGFR activity upon drug treatment.

- **Patient Samples:**  
  Preliminary data from tumor needle biopsies (pre- and on-treatment with erlotinib) demonstrated a decrease in the INKA score for EGFR, supporting the potential utility of this approach in clinical settings.

- **External Dataset Validation:**  
  INKA was also applied to publicly available phosphoproteomics datasets (e.g., for EGFR-mutant NSCLC and for other oncogene-driven tumors) where the inferred kinases corresponded well with known oncogenic drivers.

Overall, these results show that the integrative INKA score outperforms individual components and another substrate-centric tool (KARP) when it comes to identifying actionable, hyperactive kinases.

---

## 7. Validations

Multiple strategies were used to validate the approach:

- **Permutation Testing:**  
  By randomizing spectral count links and kinase–substrate annotations, null distributions were generated that allowed p values to be associated with observed INKA scores. Almost all top-ranked scores were statistically significant.

- **Comparison with Ground Truth and External Data:**  
  In cell lines with well-known oncogenic drivers, the INKA pipeline ranks these drivers at or near the top.
  
- **Validation Against Drug Sensitivity Data:**  
  Linking INKA scores with external drug sensitivity data (from resources such as the Genomics of Drug Sensitivity in Cancer, GDSC) corroborated that high INKA ranking correlated with responsiveness to specific kinase inhibitors.

- **Application on Independent Datasets:**  
  Re-analysis of literature datasets further confirmed that INKA reliably pinpoints the major active kinases.

---

## 8. Implications

The INKA pipeline has several important implications:

- **Clinical Application in Precision Oncology:**  
  Because INKA derives kinase activity profiles from single samples, it can be directly applied to patient tumor biopsies. This capability is critical for tailoring kinase inhibitor therapies to the individual tumor’s signaling landscape.

- **Improved Drug Target Prioritization:**  
  By integrating two complementary sources of evidence, the method produces a more robust and interpretable ranking of kinases, which can guide therapeutic strategies even in complex cases where multiple kinases may be active.

- **Actionable Insights Beyond Genomics:**  
  While genomic data provide key information about mutations and copy number variations, phosphoproteomics (interpreted through INKA) captures the dynamic state of signaling networks. This information can help explain instances of drug resistance or treatment failure and suggest combination therapies.

- **General Utility in Systems Biology:**  
  The method exemplifies how multiple layers of –omics data can be integrated to yield actionable, network-based biomarkers, paving the way for similar strategies in other diseases.

---

## 9. Clinical Problem Addressed

INKA addresses a critical clinical obstacle—identifying the hyperactive signaling kinases that drive individual tumors. This has several key clinical ramifications:

- **Personalized Therapy Selection:**  
  By pinpointing the active kinases in a patient’s tumor, clinicians can better select targeted therapies (or combinations thereof) that are more likely to be effective.

- **Overcoming Resistance:**  
  Because tumors often develop resistance to kinase inhibitors, having a detailed map of kinase activity may help in adjusting therapy regimens or adding second-line agents.

- **Single-Sample Utility:**  
  In the clinical context, often only a small biopsy is available. INKA’s ability to infer kinase activity from a single sample makes it a valuable tool for rapid, individualized treatment decisions.

---

## In Summary

The paper presents INKA—a novel integrative data analysis pipeline that combines kinase-centric and substrate-centric phosphoproteomic evidence to infer kinase activity in single clinical samples. Motivated by the challenge of identifying hyperactive kinases in cancer for precision therapy selection, the authors detail a framework that leverages both direct measurements and inferred substrate relationships to compute an INKA score. Validated across various cancer cell lines, differential treatment conditions, publicly available datasets, and even patient biopsies, INKA provides a robust ranking of kinase activity. The approach has significant clinical implications as it directly informs the selection of targeted therapies in oncology, addressing the crucial need for personalized treatment strategies in cancer patients.