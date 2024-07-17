# How to do gene correlation for single cell RNA-Seq data

[Blog](https://divingintogeneticsandgenomics.com/post/how-to-do-gene-correlation-for-single-cell-rnaseq-data-part-2-using-meta-cell/)
#seminar 

An approach using the meta-cell approach from an [R](R.md) package hdWGCNA is described to calculate correlation between 2 genes in different cell types. The meta-cell approach groups single cells into meta-cells. The result is better than using unprocessed single cell data that suffers from zero-inflation.

Zero-inflation describes a phenomenon in single cell data with low sequencing depth where there are many 0s in the cell-gene matrix. Because of the low sequencing depth, many genes are not detected. Having many 0s creates a [sparsity](Sparsity.md) problem.

In part 1 of the blog, the author also tries several imputation methods, but they did not improve the outcome much. It has also been reported that imputation does not improve downstream analyses such as clustering and trajectory analysis.

[Several](https://x.com/tangming2005/status/1501766040686108678) have pointed out that CD4 transcript level is low in CD4 cells, which is counter-intuitive. This could be due to a technical issue with 10x technology or the fact that the proteins are stable on the surface meaning they degrade slowly. This way a low transcript level can sustain a high protein level.