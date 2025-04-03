## Summary of the Paper: Knowledge-Guided Multi-Layer Network (KGMN)

#paper 
> metDNA2
> [metDNA2 notes](LCMS/metDNA2%20notes.md)

## Motivation

The authors were motivated by a major challenge in untargeted metabolomics: the **annotation of unknown metabolites**. While liquid chromatography–mass spectrometry (LC-MS) allows for the detection of thousands of metabolic features, annotating unknown metabolites remains difficult, as current approaches rely heavily on existing _spectral libraries and databases_, which often lack comprehensive coverage of unknown compounds. The authors aimed to address this gap by developing a network-based approach to expand metabolite annotations from known compounds to unknown ones, providing a structured framework to decipher "dark matter" in metabolomics.

---

## Key Question

- How can a network-based approach efficiently propagate metabolite annotations from known metabolites to unknowns in untargeted metabolomics datasets?
- Can this approach improve the accuracy and coverage of metabolite annotations compared to existing methods?

---

## Relevant Theories

The KGMN approach is underpinned by several key theories and principles:

1. **Metabolic Reaction Networks**:
   - Biological systems have structured pathways where metabolites are connected by enzymatic reactions. These networks (e.g., derived from KEGG) provide a knowledge-based framework that connects known metabolites to potential unknowns through their biochemical transformations.

2. **Spectral Similarity Networks**:
   - Metabolites with similar fragmentation patterns in MS/MS data are likely to be _structurally or functionally related_. This network approach clusters metabolites based on their _MS/MS spectral similarities_.

3. **Peak Correlation Networks**:
   - Chromatographic data (e.g., retention time, ionization intensity) can reveal _co-eluting_ metabolites or ion forms (adducts, isotopes). This network links features that are likely related by biological association or experimental artifact.

4. **Knowledge-Guided Multi-Layer Networking**:
   - By integrating metabolic reaction networks, spectral similarity networks, and peak correlation networks into a single framework, the authors propose a multi-layer approach to annotate unknown metabolites comprehensively and efficiently.

---

## Methods

1. **Data Integration into Multi-Layer Networks**:
   - **Layer 1**: The **knowledge-based metabolic reaction network (KMRN)** connects known metabolites (from KEGG) to unknown metabolites via in-silico generated reactions, extending the metabolic space.
   - **Layer 2**: The **knowledge-guided MS/MS similarity network** propagates annotations from known to unknown metabolites using spectral similarity and reaction-based constraints.
   - **Layer 3**: The **global peak correlation network** integrates chromatographic and mass spectrometry data to recognize ion forms (e.g., adducts, isotopes) and improve peak annotation accuracy.

2. **Automated Annotation Workflow**:
   - Seed metabolites (known compounds) are first annotated by matching LC-MS/MS data to reference libraries.
   - The network layers propagate annotations from these seeds to unknown metabolites, leveraging constraints such as reaction rules, MS/MS similarity, and peak correlations.
   - The results are validated and reported with confidence levels.

3. **Validation**:
   - The authors applied KGMN to multiple datasets, including in vitro enzymatic reactions and biological samples (e.g., human urine, plasma, liver tissue). They used repository mining, chemical standards, and in silico tools to validate annotations.

> [!info]- Confidence levels of prediction
> The paper defines the confidence levels of metabolite predictions based on the **Metabolomics Standards Initiative (MSI) guidelines**, which provide a framework for assigning confidence to metabolite annotations. Here's how they approach it:
> 
> 1. **Confidence Levels**:
>    - **Level 1**: Identifications confirmed using authentic chemical standards. This involves matching the experimental data (e.g., MS/MS spectra, retention time) with those of known standards under identical conditions.
>    - **Level 2**: Putative annotations based on high-quality spectral matches to public databases or in silico tools. These annotations are not confirmed with authentic standards but are supported by strong evidence.
>    - **Level 3**: Tentative annotations based on structural similarity or network-based relationships. These are less certain and rely on indirect evidence, such as spectral similarity or predicted biotransformations.
>    - **Level 4**: Features detected but not annotated due to insufficient information.
> 
> 1. **KGMN-Specific Confidence**:
>    - The **Knowledge-Guided Multi-Layer Network (KGMN)** assigns confidence levels to annotations by integrating multiple layers of evidence:
>      - **MS1 m/z (mass-to-charge ratio)**: Matches the precursor ion mass to known or predicted metabolites.
>      - **Retention Time (RT)**: Matches experimental RT to predicted or known values.
>      - **MS/MS Spectral Similarity**: Matches experimental fragmentation patterns to known or predicted spectra.
>      - **Biotransformation Rules**: Links metabolites through known or in silico-predicted biochemical reactions.
> 
>    - Annotations are reported with definitive confidence levels based on the combination of these criteria. For example:
>      - Metabolites with strong matches across all criteria (e.g., MS1, RT, MS/MS, and biotransformation) are assigned higher confidence.
>      - Metabolites with partial matches (e.g., MS1 and MS/MS only) are assigned lower confidence.
> 
> 1. **Validation**:
>    - The authors validate their annotations using chemical standards, public spectral libraries, and in silico MS/MS tools (e.g., MetFrag, CFM-ID, MS-FINDER). This corroboration further supports the confidence levels assigned to each metabolite.
> 
> This multi-layered approach ensures that the confidence levels reflect the robustness of the evidence supporting each annotation. 

---

## Results

1. **Annotation Efficiency**:
   - KGMN achieved a significant improvement in annotation coverage, identifying both known and previously unannotated metabolites.
   - Across diverse datasets, KGMN annotated **100–300 unknown metabolites per sample**, with >80% corroborated by in-silico MS/MS tools.

2. **Accuracy**:
   - KGMN demonstrated higher accuracy than prior approaches (e.g., MetDNA1 and CAMERA), reducing false positives caused by in-source fragments and improving the consistency of peak annotations.

3. **Validation of Unknowns**:
   - Five recurrent unknown metabolites were identified, synthesized, and validated with chemical standards, demonstrating KGMN's ability to generate reliable annotations.

---

## Key Validation Techniques

1. **Repository Mining**:
   - Putatively annotated unknowns were searched in public metabolomics repositories, showing recurrence across diverse datasets and sample types (e.g., plasma, urine).

2. **Chemical Standards**:
   - Some unknown metabolites were synthesized, and their retention times and spectra were matched to LC-MS/MS data.

3. **In Silico Tools**:
   - The annotations were corroborated using tools like MetFrag, CFM-ID, and MS-FINDER.

---

## Implications

1. **Advancing Metabolomics**:
   - By linking known metabolites to unknowns using biochemical and data-driven networks, KGMN enables a deeper exploration of the metabolome, addressing the "dark matter" problem in metabolomics.
   
2. **Broad Applicability**:
   - The KGMN framework is broadly applicable to diverse biological samples, facilitating global and scalable metabolite annotations for complex datasets.

3. **Future Developments**:
   - This network-based approach could be further expanded by integrating taxonomic data or additional reaction databases, potentially enabling species-specific metabolite annotations.

4. **Enhanced Toolkits**:
   - The approach is implemented in a freely available web server (MetDNA2), making it accessible to the research community.

---

This paper illustrates the transformative potential of a **network-based approach** to metabolite annotation, leveraging multi-layer networks to expand our understanding of the metabolome.