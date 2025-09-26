# DESeq2

## Log fold change 2 shrinkage

### Key Idea: Shrinkage of Log Fold Changes

- **Challenge with Low Counts**: For genes with very low counts, it’s hard to accurately estimate the log2 fold change (LFC). These estimates tend to be overly variable and can result in unrealistically large fold changes.
- **Solution—Shrinkage**: DESeq2 applies **LFC shrinkage**, which pulls these extreme values closer to zero. This prevents low-information genes from falsely appearing to have the largest (and most significant) fold changes.
- **Purpose**: Shrinkage ensures the results are biologically meaningful by focusing on genes with more reliable data (i.e., those with higher counts).

### Why It Matters for the MA Plot

- The shrinkage process helps the MA plot to better reflect the relationship between fold change and expression level.
- Genes with **low average normalized counts** (on the x-axis) will typically have their LFCs (on the y-axis) reduced by this shrinkage.

This adjustment ensures that significant findings are based on robust data, which is crucial for accurate interpretation of the experiment.

## GO analysis

In the Gene Ontology (GO) analysis output:

1. **Genes in Common**:
   - This refers to the number of genes from your input list (e.g., differentially expressed genes or genes of interest) that are associated with a specific GO term.
   - These are the genes from your dataset that overlap with the annotated genes in a particular GO term category.

2. **Genes in Annotation**:
   - This refers to the total number of genes that are annotated under a particular GO term in the entire genome or reference database.
   - It represents the background set of genes known to be associated with that GO term.

---

### Example

- If you analyze a list of 200 genes and find that 10 of them are associated with a GO term (e.g., "signaling receptor activity"), then:
  - **Genes in Common**: 10
  - **Genes in Annotation**: 1500 (total genes annotated with "signaling receptor activity" in the reference genome).

This helps assess the enrichment of your genes of interest within specific GO categories. 