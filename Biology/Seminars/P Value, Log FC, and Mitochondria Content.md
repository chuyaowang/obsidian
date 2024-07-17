# Bioinformatics is not (just) statistics

[Blog link](https://divingintogeneticsandgenomics.com/post/bioinformatics-is-not-just-statistics/?ck_subscriber_id=2278226863&utm_source=convertkit&utm_medium=email&utm_campaign=what%27s%20the%20p-value%20and%20log2Fold%20change%20to%20use?%20Bioinformatics%20is%20not%20(just)%20statistics%20-%2013678968)
#seminar 
## P value

For large datasets, the p value is inherently small. When thousands of cells are in each cluster, a t-test between 2 clusters to identify differentially expressed genes will result in many genes with p values of $10^{-10}$.

## Log 2 FC

To filter the significant genes based on the effect size, set a threshold with log2 fold change. The cutoff depends on how many genes are filtered and what is the effect size that is biologically significant.

## Mitochondria content

The mitochondria content is an important quality control metric. The higher it is, the more likely the cell is dead. 

The threshold is subjective. Some use 5%; some use 10%; some use 20%.

A tool called [miQC](https://www.bioconductor.org/packages/release/bioc/html/miQC.html) can be used to set a threshold based on the data. However, take note that some cells that are metabolically more active inherently have higher mitochondria content.

> metabolically active tissues (e.g., muscle, kidney) have higher mitochondrial transcript content

> For example, naive poised T cells are known to have higher ribosomal content, as are malignant cells.