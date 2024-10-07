# mRNA

## Transcription

### Sense and antisense strand

The sense strand is the top strand in [Transcription](Transcription.md). It has the same sequence as the mRNA except T is exchanged for U in mRNA. The antisense strand is the complement to the sense strand and the template for transcription.

Regulators that bind to the antisense strand can stop transcription from happening, acting as a gene [regulatory mechanism](Transcription%20Regulation.md).

### mRNA abundance

mRNA abundance is determined by 2 factors: **rate of transcription** and **rate of degradation**.
- The rate of transcription determines the rate at which transcripts are produced.
- The rate of degradation determines the rate at which transcripts are broken down.
- These rates are regulated by various factors. 
	- High expression levels are typically a result of strong promoter activity, efficient transcriptional machinery, and other regulatory factors that enhance transcription. 
	- Regulatory mechanisms, including microRNAs and RNA-binding proteins, can enhance or reduce mRNA stability and translation efficiency.
	- Processes such as RNA splicing, export from the nucleus, and degradation all influence the steady-state levels of mRNA.
- **Gene expression** in [scRNA-seq](scRNA-seq.md) is determined by the number of mRNA transcripts of a gene at the time of sampling. Genes with a high transcription rate, high mRNA stability, or both, will have a high number of mRNAs. 
## Introns and exons

The introns do not code for proteins, only the exons do. The introns must be removed in mRNA processing.

**Alternative splicing** is a mechanism that combines different exons in the same gene to produce different proteins. 

The nucleotide sequences GU and AG are splicing signals, but having those signals does not indicate mandatory splicing. Splicing only takes place at the intersection between introns and exons.

## Comparison to bacterial mRNA

A human mRNA has a special 5' cap, while a bacterial mRNA does not.
A typical human mRNA encodes one protein, while many bacterial mRNAs encode several different proteins.
A human mRNA undergoes alternative splicing, while a bacterial mRNA does not.
A human mRNA has a poly-A tail, while a bacterial mRNA does not.
Both human and bacterial mRNA contain non-coding sequences.

## Small nuclear RNA

Small nuclear RNA (snRNA) is essential for _mRNA splicing_.

## Small interfering RNA

Small interfering RNA (siRNA) mediates _degradation_ of distinct mRNAs and closing of gene loci leading to decreased gene expression.

## [Micro RNA](microRNA.md)

Micro RNA (miRNA) blocks the translation of mRNAs.
