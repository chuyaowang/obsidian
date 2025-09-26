# Enabling next-generation engineered TCR-T therapies based on high-throughput TCR discovery from diagnostic tumor biopsies

#paper 
[link](https://www.nature.com/articles/s41467-024-55420-6)

Below is a detailed summary of the key points in the paper, which describes a high-throughput, genetic screening platform for discovering tumor-specific T cell receptors (TCRs) from diagnostic tumor biopsies—aimed at enabling next-generation engineered TCR-T cell therapies.

---

## 1. Motivation

The authors set out to overcome major clinical hurdles in adoptive T cell therapy. Although tumor-infiltrating lymphocyte (TIL) therapy has produced complete and durable responses in cancers such as melanoma, its clinical broadness is hampered by several issues:  
- **Limited Availability and Viability:** Obtaining viable TILs from surgically resected tumors is difficult, and even when available, their frequency among tumor-reactive cells is low.  
- **Antigen Specificity:** Current gene-modified cell therapies (like CAR T cells) face challenges in solid tumors because of the paucity of truly tumor-specific antigens.  
- **Scalability and Patient Applicability:** There is a pressing need for methods that work on small or non-viable diagnostic biopsies and that enable the rapid identification of neoantigen-specific TCRs to produce a potent, personalized T cell product.

In summary, the motivation is to develop a method that bypasses the need for large, viable tumor fragments by enabling TCR discovery directly from diagnostic biopsies, with the ultimate goal of powering more effective and personalized TCR-T cell therapies.

---

## 2. Research Question

The central question the paper addresses is:  
**How can one efficiently and reliably identify tumor-specific, neoantigen-reactive TCRs from routine diagnostic (even non-viable) tumor biopsies to create engineered T cell therapies with high specificity and potency?**

---

## 3. Relevant Background Information

Several foundational elements set the stage for this work:

- **TIL Therapy and Its Limitations:**  
  TIL therapy has demonstrated that tumor-specific TCRs can mediate tumor eradication. However, because TILs must be harvested from resected tumor material, and given their often low frequency and dysfunctional state, the approach is not universally applicable.

- **CAR T Cell Therapy Challenges:**  
  While CAR T cells have shown high efficacy in hematological cancers, their progress in solid tumors has been modest—largely due to issues with finding targets that are truly tumor-specific and avoiding off-target effects.

- **Neoantigen Recognition:**  
  Tumor-specific mutations (neoantigens) can yield targets that are unique to cancer cells. Genetic and immunologic studies have indicated that even low-frequency TCRs within TIL repertoires can be extremely potent if they are directed against these neoantigens. However, traditional methods struggle to reliably isolate such clones.

- **High-Throughput Sequencing and Genetic Screening:**  
  Advances in next-generation sequencing have already made it possible to capture the TCR repertoire from tumor samples. However, going from thousands of TCR sequences to determining which ones are functionally antigen reactive has been a major bottleneck.

> [!info]- TCR and T Cell Therapy
> T cell receptors (TCRs) are proteins expressed on the surface of T cells that play a crucial role in the adaptive immune system. Their main functions and roles in cell therapies can be summarized as follows:
> 
> ---
> 
> ### What Are T Cell Receptors?
> 
> - **Structure and Composition:**  
>   TCRs are typically heterodimers composed of two chains—most commonly an alpha and a beta chain. These chains possess variable regions (especially within the complementarity-determining regions, or CDRs) that determine the receptor’s specificity.
> 
> - **Antigen Recognition:**  
>   TCRs recognize short peptide fragments (antigens) that are presented on the surface of cells by major histocompatibility complex (MHC) molecules. This recognition is highly specific; every TCR is “tuned” to bind a particular peptide–MHC combination.  
>   - For example, infected or cancerous cells will process proteins internally and present fragments derived from these proteins on their MHC molecules. A T cell bearing the corresponding TCR will then bind to this complex and become activated.
> 
> - **Activation of T Cells:**  
>   Once a TCR successfully engages with its antigen–MHC complex, it triggers intracellular signaling cascades that activate the T cell. Activated T cells can then proliferate and differentiate into effector cells that kill target cells or help orchestrate broader immune responses.
> 
> ---
> 
> ### How Are T Cell Receptors Used in T Cell Therapies for Cancer?
> 
> - **Adoptive Cell Therapy Approach:**  
>   In cancer, one strategic approach is to harness or reprogram T cells to recognize tumor-specific antigens:
>   - **Isolation:** T cells are isolated from the patient, either from the peripheral blood or directly from tumor tissue (e.g., tumor-infiltrating lymphocytes, or TILs).
>   - **Genetic Engineering:** These T cells can be genetically modified to express TCRs that are specific for antigens present on tumor cells. This modification can be achieved by introducing genes encoding for well-characterized, tumor-reactive TCRs into a patient’s T cells.
>   - **Expansion and Reinforcement:** Once engineered, the T cells are expanded ex vivo (in the laboratory) to generate enough cells. They are then re-infused into the patient, where they seek out and kill cells presenting the tumor-specific antigens on their MHC molecules.
> 
> - **Advantages of TCR-Based Therapies:**  
>   - **Broader Target Spectrum:** Unlike chimeric antigen receptors (CARs), which are typically limited to recognizing surface proteins, TCRs can detect intracellular proteins once they are processed and presented as peptides on MHC molecules. This greatly expands the repertoire of potential tumor targets, including neoantigens (mutated peptides) that are unique to cancer cells.
>   - **Personalization:** The inherent diversity of TCRs allows for personalized therapies. By identifying and selecting TCRs from the tumor microenvironment (or even by screening large libraries), clinicians can tailor the therapy to target the specific antigens expressed by a patient’s tumor.
>   - **Potential in Solid Tumors:** Although CAR T cell therapies have achieved remarkable successes in certain blood cancers, TCR-based therapies hold promise particularly for solid tumors where many potentially immunogenic intracellular antigens exist.
> 
> - **Clinical Application and Challenges:**  
>   The goal of TCR-T cell therapies is to create a highly specific and effective T cell product that can recognize and eliminate cancer cells while sparing healthy tissues. However, because TCRs are MHC-restricted, their efficacy depends on the patient’s HLA type and on the tumor’s ability to present antigens. Additionally, ensuring a sufficient level of T cell activation without triggering autoimmunity remains a key challenge.
> 
> ---
> 
> ### In Summary
> 
> - **T cell receptors** are the natural antigen-recognition molecules on T cells. They bind to peptides displayed by MHC molecules on target cells, initiating T cell activation.
> - **In cancer therapies,** TCRs are harnessed by engineering T cells to express receptors that are specific for tumor-associated or neoantigen-derived peptides. This enables the T cells to recognize and eliminate cancer cells effectively.
> - **Why it Matters:** By extending target recognition to intracellular proteins (via peptide presentation on MHC), TCR-based therapies expand the range of cancers that can be targeted and offer a promising avenue for personalized immunotherapy—especially in solid tumors where traditional approaches may fall short.
> 
> This strategy forms a central pillar of emerging T cell therapies that seek to improve outcomes for cancer patients by leveraging the exquisite specificity and potency of the immune system.
> 
> This background provides the rationale for merging comprehensive sequencing of TCR repertoires with a sensitive, pooled functional genetic screen to pinpoint the TCRs that drive anti-tumor responses.

---

## 4. Relevant Theories

The work builds on a number of theoretical principles:

- **Immunogenomics and Antigen Presentation:**  
  The theory that the specificity and efficacy of a T cell response are determined by the precise recognition of antigens presented by HLA molecules. This includes both HLA class I– and class II–restricted pathways, which are crucial for orchestrating CD8+ and CD4+ T cell responses.

**Human Leukocyte Antigen (HLA) molecules** are proteins encoded by genes in the major histocompatibility complex (MHC) region on chromosome 6. They play a critical role in the immune system by presenting peptide fragments—derived either from within the cell or from external sources—to T lymphocytes. This process is essential for the body to distinguish self from non-self and to trigger appropriate immune responses.

> [!info]- HLA Molecule
> ### 1. HLA Molecules: Overview
> 
> - **Nature and Function:**  
>   HLA molecules are the human version of MHC proteins. They are found on the surface of most cells and are responsible for “displaying” peptide fragments that have been generated from protein degradation. This display allows T cells to “inspect” the peptides and determine whether the cell is healthy, infected, or transformed (as in cancer).
> 
> - **Polymorphism:**  
>   The HLA genes are highly polymorphic, meaning there is a vast diversity of alleles in the human population. This diversity is vital because it enables the immune system to present a wide array of peptides, accommodating the variability of pathogens and abnormal cells.
> 
> ---
> 
> ### 2. HLA Class I Molecules and the Endogenous Pathway
> 
> - **Expression Pattern:**  
>   HLA class I molecules are expressed on almost all nucleated cells in the body.
> 
> - **Structure:**  
>   They consist of a heavy (alpha) chain along with β2-microglobulin, a smaller subunit. The polymorphic nature of the alpha chain determines which peptides are bound.
> 
> - **Peptide Source and Presentation:**  
>   These molecules primarily present peptides derived from proteins within the cell (the endogenous pathway). Proteins—whether normal, mutated, or viral—are degraded by the proteasome into peptide fragments.  
>   - **Loading Process:** Peptides are transported into the endoplasmic reticulum (ER) by the transporter associated with antigen processing (TAP), where they are loaded onto HLA class I molecules.  
>   - **T Cell Interaction:** Once on the cell surface, these peptide–HLA class I complexes are recognized by CD8⁺ cytotoxic T lymphocytes. This interaction is crucial, for example, in the detection and destruction of virus-infected or cancerous cells.
> 
> ---
> 
> ### 3. HLA Class II Molecules and the Exogenous Pathway
> 
> - **Expression Pattern:**  
>   Unlike class I, HLA class II molecules are mainly expressed on professional antigen-presenting cells (APCs) such as dendritic cells, macrophages, and B cells.
> 
> - **Structure:**  
>   They are heterodimers made of an alpha and a beta chain. The structure of the peptide-binding groove in HLA class II molecules is suited to accommodate longer peptides.
> 
> - **Peptide Source and Presentation:**  
>   These molecules present peptides that are usually derived from proteins taken up from outside the cell (the exogenous pathway).  
>   - **Uptake and Processing:** Extracellular antigens are internalized through processes like phagocytosis or endocytosis. These proteins are then degraded in endosomal/lysosomal compartments.  
>   - **Loading Process:** In these compartments, peptides are loaded onto HLA class II molecules after the invariant chain (which occupies the binding groove during synthesis) is removed.  
>   - **T Cell Interaction:** The resulting peptide–HLA class II complexes are presented on the cell surface, where they are recognized by CD4⁺ helper T cells. This recognition triggers further immune responses such as the activation of B cells and orchestration of other immune effectors.
> 
> ---
> 
> ### 4. HLA Restriction in Antigen Presentation
> 
> - **HLA Class I–Restricted Pathway:**  
>   - **Mechanism:** Endogenous proteins are processed in the cytosol and loaded onto HLA class I molecules in the ER.  
>   - **Function:** This pathway is primarily responsible for the surveillance of intracellular health, enabling cytotoxic T cells to target and eliminate cells harboring mutations, infections, or neoplastic changes.
>   
> - **HLA Class II–Restricted Pathway:**  
>   - **Mechanism:** Exogenous proteins, once internalized and processed in endosomal compartments, are loaded into HLA class II molecules.  
>   - **Function:** This pathway plays a central role in activating helper T cells, which in turn coordinate the overall immune response by assisting other immune cells such as B cells (for antibody production) and complementing the cytotoxic response.
> 
> ---
> 
> ### Clinical Significance
> 
> Understanding HLA class I and class II pathways is central to many clinical applications:
> - **Transplantation:**  
>   Differences in HLA types between donors and recipients are a primary cause of transplant rejection.
> - **Cancer Immunotherapy:**  
>   T cell therapies, including those using engineered TCRs, rely on proper HLA-peptide presentation to target tumor cells while minimizing off-target effects.
> - **Infectious Diseases and Autoimmunity:**  
>   HLA diversity influences susceptibility to infections and the propensity for certain autoimmune disorders, as the presented peptide repertoire shapes the immune system’s tolerance and reactivity.
> 
> In summary, HLA molecules are critical for the immune system’s ability to detect and respond to abnormal cells. HLA class I molecules present intracellular (endogenous) peptides to CD8⁺ T cells, while HLA class II molecules present extracellular (exogenous) peptides to CD4⁺ T helper cells. Together, these pathways ensure a robust and balanced immune response, which is essential for both defending against pathogens and for developing targeted therapies, such as T cell therapies for cancer.

- **T Cell Activation as a Functional Readout:**  
  The notion that TCR triggering, which can be sensitively measured (e.g., by upregulation of activation markers such as CD69), is a reliable indicator of a T cell’s ability to recognize its cognate antigen. By coupling TCR expression to a single functional assay, one can use enrichment analysis to home in on the antigen-specific clones.

- **Pooled Functional Genetic Screening:**  
  Based on concepts borrowed from CRISPR/Cas9 screens or drug-resistance screenings, where changes in the abundance of specific constructs (here, TCR sequences) after selection (via activation) indicate their functional importance. Statistical enrichment of a TCR in the activated pool offers proof of antigen specificity.

These theories provide both the biological foundation and the methodological rationale for the approach.

---

## 5. Methods

The paper outlines a multi-step, high-throughput pipeline:

1. **Tumor Profiling and TCR Repertoire Acquisition:**  
   - **Next-Generation Sequencing (NGS):** Genomic and RNA sequencing of diagnostic tumor biopsies (including non-viable, frozen core-needle biopsies) is performed. This step identifies both the tumor-specific non-synonymous mutations (neoantigens) and the intratumoral TCRα and TCRβ repertoires.

2. **Synthetic Library Assembly:**  
   - **TCR and Neoantigen Library Generation:** Using synthetic biology tools, the researchers assemble combinatorial TCR libraries that combine TCRα and TCRβ chains identified from the biopsy. Simultaneously, neoantigens are encoded in tandem minigene (TMG) constructs.

3. **Functional Genetic Screening:**  
   - **Expression in Reporter Cells:** The combinatorial TCR library is introduced into reporter T cells.
   - **Antigen Presentation:** Autologous antigen-presenting cells (B cells) are engineered to express TMGs representing candidate neoantigens.
   - **Coculture and Activation:** TCR-transduced reporter T cells are cocultured with the TMG-expressing B cells. Activation is measured by assessing markers such as CD69.
   - **Sorting and NGS Readout:** Activated (and non-activated) cells are sorted, and TCR sequences are recovered by PCR and quantified via NGS. Significant enrichment of certain TCRs in the activated pool identifies candidate neoantigen-specific receptors.

4. **Validation and Characterization:**  
   - **In Vitro T Cell Assays:** Candidate TCRs are subsequently validated by performing co-culture experiments with APCs and using peptide titration assays.
   - **HLA Restriction Determination:** Additional experiments (including CRISPR/Cas9-mediated B2M knockout and antibody blocking) confirm whether the TCRs are HLA class I– or class II–restricted and verify mutation specificity.

---

## 6. Results

The study reports several major findings:

- **Efficient TCR Discovery:**  
  The platform reliably identified antigen-specific TCRs from pools that included thousands of TCR clonotypes—even when the tumor sample was non-viable. In test cases with melanoma and other indications, hundreds to thousands of clonotypes were detected, and functional screening identified multiple candidate TCRs.

- **High Sensitivity and Specificity:**  
  The enrichment analysis was able to detect neoantigen-specific TCRs even when present at very low frequencies (as low as 1 in 100,000 cells). In validation experiments, a very high percentage (e.g., 96% in one set) of candidate TCRs showed clear and specific reactivity to their cognate neoantigens over the corresponding wild-type peptides.

> [!info]- How sensitivity is validated
> The “frequencies” here refer to the dilution ratios at which the Jurkat reporter T cells that express the defined antigen‐specific TCRs (CDK4_17 and CDK4_8) are present in the overall cell mixture. In practical terms, a frequency of 1:10 means that one out of every 10 reporter T cells expresses the antigen‐specific TCR, while 1:10,000 indicates that only one in 10,000 cells carries that receptor.  
> 
> In this experiment, the researchers mixed these defined antigen‐specific TCR‐expressing cells at various dilution levels (from 1:10 to 1:10,000) with other T cells that do not have these TCRs. This was done to test how sensitive their assay is at detecting T cell activation when antigen‐specific cells are very rare. They then cocultured these mixed populations with EBV‐immortalized B cells that were loaded with either a non-cognate (irrelevant) or a cognate CDK4 peptide. By staining for the activation marker CD69 and analyzing via FACS, they could determine if the antigen‐specific T cells (even when rare, e.g., at a 1:1000 dilution) became activated in the presence of their specific antigen.
> 
> In summary:  
> - **Frequencies/dilutions (1:10 to 1:10,000)** represent the proportion of antigen-specific TCR-expressing cells within the reporter T cell pool.  
> - **1:1000 dilution shown as data** means that in that particular experiment, the defined antigen-specific cells were present at a ratio of one in every 1,000 cells, demonstrating the assay's sensitivity to detect activation (via CD69 expression) even when the target cells are very low in frequency.

- **Broad Applicability:**  
  The approach was successfully applied not only to melanoma, a tumor type with high mutational burden, but also to microsatellite-stable colorectal cancer (a low TMB cancer), non-small-cell lung cancer, and even virus-associated tumors like Merkel cell carcinoma. Both HLA class I and HLA class II responses were detected.

---

## 7. Validations

To ensure the robustness of their approach, the authors undertook several validation steps:

- **Functional Assays:**  
  Reporter T cell activation (as measured by CD69 upregulation and other markers) was used as the primary readout to validate TCR reactivity.

- **Peptide Electroporation Experiments:**  
  These assays deconvoluted the specific epitope recognized by each TCR, confirming the precise neoantigen specificity.

- **HLA Restriction Studies:**  
  By using CRISPR/Cas9 knockout models (targeting B2M) and blocking antibodies, the researchers determined whether the responses were mediated by HLA class I or class II.

- **Positive Controls and Statistical Significance:**  
  A well-characterized positive control TCR (such as CDK4-17) was used to benchmark the screening method, and rigorous statistical analyses (with Bonferroni correction) confirmed the reliability of the enrichment readouts across multiple independent experiments.

---

## 8. Implications

The innovation described in this study has broad implications:

- **Advancement in T Cell Therapy:**  
  By providing a streamlined method for high-throughput harvest and screening of antigen-specific TCRs, the platform could greatly expand the available pool of tumor-reactive TCRs. This will enable the development of more effective and personalized engineered TCR-T cell products.

- **Overcoming Sample Limitations:**  
  The ability to work with non-viable, frozen diagnostic biopsies opens up access to patient samples that were previously not suitable for TIL isolation, broadening the patient population that might benefit from adoptive cell therapies.

- **Precision Immunotherapy:**  
  The platform permits the isolation of TCRs with high specificity—even for low-frequency neoantigens. This precision could translate into T cell products that have superior tumor recognition while minimizing the risk of off-target effects.

---

## 9. Clinical Problem Addressed

The clinical challenge at the heart of this work is the limited efficacy of current T cell therapies in solid tumors, partly due to the difficulty of isolating potent, tumor-specific T cells and the constraints of working with viable tumor tissue. By establishing a method that identifies neoantigen-specific TCRs from small or non-viable diagnostic samples, this innovation:
- **Enables Personalized TCR-T Cell Therapies:** Tailored T cell products can be manufactured even when traditional TIL therapy is not feasible.
- **Improves Outcomes in Solid Tumors:** With more robust targeting of tumor-specific neoantigens, patients with cancers such as melanoma, colorectal cancer, lung cancer, or virus-associated tumors may see improved clinical responses.
- **Extends Immunotherapy to a Broader Range of Patients:** By overcoming the limitations of sample viability and TCR abundance, the approach may make advanced immunotherapies accessible to patients who were previously ineligible.

---

In summary, the paper presents a comprehensive, high-throughput platform that integrates genomic sequencing, synthetic library assembly, pooled functional screening, and rigorous validation methodologies to identify tumor-specific TCRs from routine diagnostic biopsies. This work is motivated by the need to overcome current obstacles in adoptive T cell therapy for solid tumors, employs contemporary theories of immunogenomics and functional screening, and shows promising results that may lead to more personalized and effective cancer immunotherapies.