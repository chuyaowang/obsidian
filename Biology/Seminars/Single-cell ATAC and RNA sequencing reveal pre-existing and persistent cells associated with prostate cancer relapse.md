# scRNA and scATAC for studying prostate cancer drug resistance

[Paper](https://www.nature.com/articles/s41467-021-25624-1)
[scRNA-seq](scRNA-seq.md)
[scATAC-seq](scATAC-seq.md)
Uses cell line data, not tissue sample
## Introduction

- **Androgen receptor (AR)**: a type of nuclear receptor that is activated by binding to androgens, which are male hormones such as testosterone and dihydrotestosterone (DHT). Androgens promote prostate cancer cell growth.
- **ENZ**: Enzalutamide is an anti-androgen drug that inhibits AR signaling through several mechanisms such as competitive binding and downstream interference of the signaling pathway. Prolonged use of ENZ make the cancer cells adapt to low androgen environment.
	- CRPC (Castration-Resistant Prostate Cancer): cancer cells evolve to be more easily activated, express more copies of AR, or does not bind ENZ but still binds androgens.
	- NEPC (Neuroendocrine Prostate Cancer): cancer cells evolve to be no longer depend on androgens to grow.
		- NEPC cells lose their reliance on androgen signaling and gain neuroendocrine features, characterized by the expression of neuroendocrine markers such as chromogranin A, synaptophysin, and neuron-specific enolase (NSE).
		- They become reliant on neuroendocrine for promoting growth.
- **LNcaP cells**: a prostate cancer cell line that is known for its sensitivity to androgens. It produces prostate-specific antigens that can be used as markers for prostate cancer.
- **Androgen starvation**: reducing the amount of androgen available to cancer cells. Initially growth is suppressed. Resistance develops later.
- [MYC Signaling](MYC%20Signaling.md)
- **Binding site map**: 
## Result

### Chromatin reprogramming underpins ENZ resistance

- Chromatin accessibility observed in ENZ-resistant cells: 
	- The ATAC-seq signal at transcription-start sites (TSS) decreased in ENZ-resistant cells compared with the parental
	- RES-A and RES-B cells shared a large proportion of ENZ-resistance-specific open-chromatin regions not found in parental LNCaP
	- the chromatin of ENZ-resistant cells is more open in the presence of androgens (_p_ < 0.001, _t_-test) (Supplementary Fig. [1e](https://www.nature.com/articles/s41467-021-25624-1#MOESM1)) and in castrate conditions
		- In castrate condition, cells evolve to grow without androgens.
		- Being resistant to ENZ makes them respond to androgen again?
		- _Idea: Compare parental (LNcaP) with resistant cell lines_
- Clustered **all** cells by their chromatin accessibility profile
	- Identified proportions of cells from each group in each cluster
	- Unique clusters for RESA and RESB are named **ENZ-induced clusters**
	- Unique clusters for DMSO and ENZ48 are named **initial clusters**
	- **Persistant clusters**: similar proportions across the groups
	- 74% of the cells share an overall similar chromatin-accessibility profile during the development of ENZ resistance
	- [Differentially Accessible Regions](scATAC-seq.md#Differentially%20Accessible%20Regions) (DARs) were observed around _MYC_ and _TP53_ in several clusters during the short-term response to enzalutamide
- Neuroendocrine behavior in ENZ resistant cells
	- The largest fold changes in chromatin accessibility based on average signal from all cells showed **over representation for neuronal system processes** between the parental (LNCaP or LNCaP–ENZ48) and resistant cells (RES-A or RES-B)
	- Accordingly, we found elevated expression of NEPC-derived signatures in RES-A and RES-B cells (particularly _EZH2_, _AURKA_, _STMN1_, _DNMT1_, and _CDC25B_), as well as increased expression of NEPC-downregulated genes in initial clusters


| Cluster | Type        |
| ------- | ----------- |
| 0       | Persistant  |
| 1       | Persistant  |
| 2       | Persistant  |
| 3       | Persistant  |
| 4       | Initial     |
| 5       | Persistant  |
| 6       | ENZ-induced |
| 7       | ENZ-induced |


### ENZ resistance reconfigures availability of TF binding DNA motifs in the chromatin

After finding chromatin reprogramming happens in ENZ resistant cells, they found the availability of TF binding [motifs](1.%20MIT%20CompBio%20-%20Introduction.md#^6a1795) change in these cells.

A motif is a sequence of DNA that has a biological function, like binding [TFs](Transcription%20Factor.md).

Opening the chromatin exposes the TF binding motifs within. Hence, they studied the difference in the binding motifs within the [Open Chromatin Regions](Open%20Chromatin%20Regions.md) among the groups.

They observed a significant increase in open chromatin at [MYC](MYC%20Signaling.md)-binding sites in ENZ-resistant cells. MYC are a family of TFs that are oncogenic. They also observed a reduction of open chromatin at AR-binding sites in **castrate** conditions, and an increase in open chromatin at AR-binding sites in androgen-exposed conditions.

These findings align with previous reports that in ENZ resistant cells MYC signaling increases and AR signaling decreases. This could be understood as a compensatory mechanism to adapt to androgen scarcity.

For each cell cluster based on scATAC profile, a set of marker DARs were identified. Those DARs would open up some TF binding motifs. TF binding motif enrichment analysis confirmed the enrichment of motifs for several PC-associated TFs such as AR and MYC. There are more, read the paper for details.

Comparing open DARs in RES-A or RES-B to the LNCaP parental retrieved distinct sets of TFs, with _MYC_ and _ESR1_ being the most common across all clusters in RES-A and RES-B. Similarly, comparing open DARs in RES-A or RES-B vs LNCaP–ENZ48 showed enrichment of most of the PC-related TF motifs tested in most clusters
### Transcriptional patterns of ENZ resistance are induced by divergent chromatin reprogramming

Did scRNA sequencing to verify if chromatin reprogramming leads to transcriptional differences.

Used [Cluster Label Transfer](Cluster%20Label%20Transfer.md) and different cell lines to verify if results observed in LNCaP cell line is generalizable.

Clustered LNCaP parental, RESA, RESB, ENZ48 after integrating them. Identified 7 persistant, 3 ENZ-induced, and 3 initial clusters, a total of 13 scRNA clusters. _Idea: just study how cell states shift among three cluster types. Use bioib to do functional difference among the clusters_.

scRNA seq confirms chromatin reprogramming induces transcriptional changes. Using annotated databases, they queried the **transcriptional targets** of the enriched TFs in the open DARs when comparing RES-A or B to the parental LNCaP in the matching scRNA-seq samples. DAR: differentially accessible regions between RESA or B and parental LNCaP.

Used cluster label transfer again to transfer label from scRNA clusters to scATAC clusters and vice versa. Found that one chromatin state can correspond to multiple transcriptional state.

### Prostate cancer cell subpopulations with features of stemness precede ENZ resistance

Used Seurat to score the clusters for their [Cell Cycle](Cell%20Cycle.md) stage. 
- Identified _persistent_ clusters are more actively cycling and proliferating.
- They are also characterized by genes associated with stemness, chromatin remodeling and organization, and DNA repair; considering they are actively cycling, it makes sense.
- This set of genes defined as Persist
Another set of genes that promotes tissue regeneration defined as PROSGenesis. Found PROSGenesis in _initial cluster_ 10

Analyzed how cell clusters develop:
- CytoTRACE: ranks developmental potential
- RNA velocity analysis




