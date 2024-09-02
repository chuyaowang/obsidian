# FAIRE-seq: Formaldehyde-Assisted Isolation of Regulatory Elements Sequencing

**FAIRE-seq** is a genomic technique used to identify [Open Chromatin Regions](Open%20Chromatin%20Regions.md), which are often associated with active regulatory elements such as [Promoter](Promoter.md)s, [Enhancer](Enhancer.md)s, and other [Transcription Factor](Transcription%20Factor.md) binding sites. The method leverages the fact that open chromatin regions are more accessible and less tightly bound to nucleosomes compared to closed chromatin regions.

## Steps

1. **Crosslinking:**
   - Cells are treated with formaldehyde, which crosslinks proteins to DNA, thereby preserving protein-DNA interactions in both open and closed chromatin regions.

2. **Chromatin Fragmentation:**
   - The crosslinked chromatin is then sheared into small fragments using sonication or other mechanical methods.

3. **Phenol-Chloroform Extraction:**
   - The fragmented chromatin is subjected to phenol-chloroform extraction, a method used to separate proteins from DNA. Open chromatin regions, which are less protein-bound, preferentially partition into the aqueous phase, whereas the protein-bound (closed) chromatin remains in the organic phase.

4. **DNA Purification:**
   - The DNA from the aqueous phase is purified. This DNA represents the regions of open chromatin.

5. **Sequencing:**
   - The purified DNA is then subjected to high-throughput sequencing. The sequencing reads are aligned to a reference genome to identify the genomic locations of open chromatin regions.

## Applications of FAIRE-seq

1. **Identification of Regulatory Elements:**
   - FAIRE-seq is used to map active [regulatory elements](Transcription%20Regulation.md) such as promoters, enhancers, and insulators across the genome.

2. **Comparison of Chromatin States:**
   - By comparing FAIRE-seq profiles under different conditions or in different cell types, researchers can identify changes in chromatin accessibility associated with various biological processes or diseases.

3. **Gene Regulation Studies:**
   - FAIRE-seq helps in understanding the regulatory architecture of the genome and how changes in chromatin accessibility affect gene expression.

4. **Cancer Research:**
   - In cancer research, FAIRE-seq can be used to identify regulatory elements that are aberrantly activated or repressed in cancer cells, providing insights into mechanisms of oncogenesis and potential therapeutic targets.

## Advantages of FAIRE-seq

1. **High Resolution:**
   - FAIRE-seq provides high-resolution maps of open chromatin regions, enabling precise identification of regulatory elements.

2. **No Antibodies Required:**
   - Unlike ChIP-seq (Chromatin Immunoprecipitation sequencing), which requires specific antibodies for the target proteins, FAIRE-seq does not rely on antibodies, making it more straightforward and less biased.

3. **Applicability to Various Conditions:**
   - FAIRE-seq can be applied to any cell type or condition, allowing for broad utility in different biological contexts.

## Comparison with Other Techniques

1. **DNase-seq:**
   - DNase-seq uses DNase I to digest accessible chromatin regions and identifies them through sequencing. It also maps open chromatin but can have different biases compared to FAIRE-seq.

2. **ATAC-seq:**
   - [ATAC-seq](scATAC-seq.md) (Assay for Transposase-Accessible Chromatin using sequencing) uses a transposase enzyme to insert sequencing adapters into open chromatin regions. It is faster and requires fewer cells compared to FAIRE-seq and DNase-seq.

## vs. ATAC-seq

**FAIRE-seq** and **ATAC-seq** are both techniques used to map open chromatin regions in the genome. However, they differ in their methodologies, sensitivities, and specific applications.

### FAIRE-seq

**Methodology:**
1. **Crosslinking:** Cells are treated with formaldehyde to crosslink proteins to DNA, preserving protein-DNA interactions.
2. **Chromatin Fragmentation:** The chromatin is sheared into small fragments using sonication.
3. **Phenol-Chloroform Extraction:** The fragmented chromatin is subjected to phenol-chloroform extraction to separate open chromatin regions into the aqueous phase.
4. **DNA Purification:** The DNA from the aqueous phase is purified and sequenced.

**Advantages:**
1. **No Specific Antibodies Required:** Unlike ChIP-seq, FAIRE-seq does not require specific antibodies, reducing bias and simplifying the procedure.
2. **Broad Applicability:** Can be applied to various cell types and conditions without needing specific reagents for each context.

**Disadvantages:**
1. **Lower Sensitivity:** FAIRE-seq may have lower sensitivity compared to ATAC-seq, especially for regions with moderate accessibility.
2. **Formaldehyde Crosslinking:** The requirement for formaldehyde crosslinking can introduce variability and requires careful handling.

### ATAC-seq

**Methodology:**
1. **Transposase Tagmentation:** A transposase enzyme inserts sequencing adapters into regions of open chromatin.
2. **Fragmentation:** The transposase simultaneously fragments the DNA and adds adapters, targeting accessible regions.
3. **Sequencing:** The tagmented DNA is purified and sequenced.

**Advantages:**
1. **High Sensitivity:** ATAC-seq is _highly sensitive_ and can detect regions with varying degrees of chromatin accessibility, including those that are less accessible.
2. **Low Input Requirement:** Requires fewer cells and less starting material compared to FAIRE-seq.
3. **Rapid Protocol:** The entire procedure is faster, often taking less than a day from cell preparation to library preparation.

**Disadvantages:**
1. **Transposase Bias:** The transposase enzyme may introduce some sequence bias, affecting the uniformity of chromatin accessibility detection. Meaning the transposase may prefer some open regions than others.
2. **Cost:** ATAC-seq can be more expensive due to the specialized reagents and equipment required.

### Applications and Suitability

**FAIRE-seq:**
- **Broad Mapping of Open Chromatin:** Suitable for general mapping of open chromatin regions, particularly in studies where antibody specificity is a concern.
- **Historical Use:** Has been a standard method for many years and is well-established in the literature.
- **Comparative Studies:** Can be used alongside other techniques to validate findings or to study chromatin accessibility under different conditions.

**ATAC-seq:**
- **High-Resolution and Sensitivity:** Ideal for high-resolution mapping of chromatin accessibility, including fine-scale variations.
- **Single-Cell Applications:** ATAC-seq can be adapted for single-cell applications (scATAC-seq), enabling the study of chromatin accessibility at the single-cell level.
- **Quick Turnaround:** Useful in time-sensitive studies due to its rapid protocol.

### Summary

Both FAIRE-seq and ATAC-seq are valuable for mapping open chromatin regions, but they have distinct advantages and limitations. FAIRE-seq is a robust, broadly applicable method with no need for specific antibodies, while ATAC-seq offers higher sensitivity, requires less input material, and can be adapted for single-cell analysis. The choice between the two techniques depends on the specific requirements of the study, including the desired sensitivity, resolution, and throughput.