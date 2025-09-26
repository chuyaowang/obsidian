# New treatment alternatives for primary and metastatic colorectal cancer by an integrated transcriptome and network analyses

#paper 
[link](https://www.nature.com/articles/s41598-024-59101-8)

## 1. Motivation

Metastatic colorectal cancer (CRC)—especially liver metastasis—remains a major clinical challenge despite existing therapeutic options such as chemotherapy, immunotherapy, and targeted treatments. Many patients with advanced CRC do not respond well to current therapies. This study is motivated by the need to identify novel therapeutic targets and treatment alternatives for both primary CRC and its liver metastases. By leveraging integrated transcriptome analyses and network-based approaches, the authors aim to discover biomarkers that not only shed light on the mechanistic differences between primary and metastatic tumors but also point toward candidate drugs that may inhibit cancer proliferation or metastatic behavior.

---

## 2. Research Question

The central question addressed is:  
**How can integrated transcriptome profiling and gene co-expression network analyses be used to identify new therapeutic targets and alternative drugs for both primary and liver metastatic colorectal cancer?**

In essence, the study seeks to develop a holistic in-silico workflow that:
- Identifies gene modules associated with distinct CRC phenotypes (normal colon, primary CRC, and liver metastasis),
- Pinpoints candidate biomarkers through network clustering and pathway enrichment analyses, and
- Cross-links these biomarkers to potential therapeutic drugs via drug–target interaction searches, with subsequent in-vitro validation.

---

## 3. Relevant Background Information

### Gene Expression Data & Acquisition

- **Data Sources:**  
  The study makes extensive use of microarray data acquired from multiple publicly available Gene Expression Omnibus (GEO) datasets. These datasets represent samples from normal colon tissue, primary colorectal cancer, and liver metastases of CRC.
  
- **Data Integration:**  
  The authors integrated these microarray samples to create larger cohorts—termed “training” and “validation” sets—ensuring that findings were robust across independent sample collections.

### Transcriptome and Network Analyses

- **Co-expression Analysis:**  
  The study employs Weighted Gene Co-expression Network Analysis (WGCNA). WGCNA is an established method that constructs networks based on the co-expression of genes to reveal modules (clusters) of genes whose expression patterns correlate with clinical phenotypes (e.g., primary vs. metastatic).
  
- **Network Clustering & Enrichment:**  
  After identifying significant modules via WGCNA, the authors further subdivide these modules using various network clustering algorithms (e.g., Markov Clustering, Fuzzy Neighborhood, Spectral Clustering, Infomap, and Label Propagation). The goal is to extract submodules that are biologically homogeneous and enriched in the context of each phenotype.
  
- **Pathway and Functional Enrichment:**  
  Gene set enrichment analyses (using KEGG, GO Biological Process, and Cancer Hallmark terms) were performed on each module to determine which cellular pathways and biological processes are most affected. This enables prioritization of candidate genes that are not only differentially expressed but are also functionally implicated in tumor progression or metastasis.

---

## 4. Relevant Theories

Several conceptual frameworks ground the study’s design and interpretation:

- **Co-expression and Modular Organization Theory:**  
  The idea that genes do not function in isolation but in coordinated networks is central. WGCNA is founded on the theory that genes with similar expression patterns (modules) are likely to participate in related biological functions or signaling pathways.

- **Network Clustering and Hub Gene Identification:**  
  Within large networks, certain submodules or clusters may serve as “hotspots” of dysregulation. This theory extends to the notion that hubs (genes with many connections) or modules enriched for specific pathway activities can be the drivers of disease phenotypes—in this case, CRC progression and metastasis.

- **Drug-Repositioning Based on Network Pharmacology:**  
  By mapping the affected networks to drug–target databases (such as DGIdb), the study rests on the idea that targeting network hubs or critical pathway nodes with known compounds can yield effective therapeutic alternatives. This integrative approach merges systems biology with pharmacology.

---

## 5. Methods

The study unfolds in several key steps:

1. **Integrated Transcriptome Analysis:**  
   - Microarray datasets from various GEO sources were harmonized and integrated.
   - WGCNA was applied to the training dataset to build robust gene co-expression networks.  
   - A soft thresholding power was computed to ensure a scale-free network topology. Modules (22 initially) were identified and merged based on similarity, and six modules were selected based on their Pearson correlations and p-values with specific sample phenotypes (e.g., primary CRC, liver metastasis).

2. **Network Clustering & Submodule Selection:**  
   - Tissue-specific networks (FINs) were constructed for different phenotypes (normal colon, primary CRC, metastasis).
   - Several clustering algorithms were applied. For each phenotype, clustering performance was evaluated using metrics such as the Biological Homogeneity Index (BHI) and biological pathway enrichment scores.
   - Key submodules were then isolated for downstream candidate biomarker selection.

3. **Gene Set Enrichment & Biomarker Selection:**  
   - Differential expression analyses were performed within the significant submodules.
   - Pathway enrichment identified key biological processes—for example, cell cycle regulation, p53 signaling, and EMT (epithelial-mesenchymal transition).
   - From these analyses, sets of genes were nominated as potential biomarkers for primary CRC as well as for the transition from primary CRC to liver metastasis.

4. **Drug-Target Interaction Screening:**  
   - The shortlisted biomarkers were input into the Drug-Gene Interaction Database (DGIdb) to identify drugs that can target these proteins.
   - A specific focus was on compounds affecting cell cycle regulation for primary CRC (e.g., Hesperadin and BAY-1217389, which target TTK and NEK2) and on agents for metastatic CRC (e.g., IL-29A, also referred to as Peginterferon-λ-1a).

5. **Experimental (In-Vitro) Validation:**  
   - The candidate drugs were tested in-vitro across CRC cell lines.
   - For anti-proliferative agents, cell viability was measured using the WST-1 assay, colony formation assays were conducted over 14 days, and proliferation was assessed via Ki-67 immunofluorescence.
   - Cell cycle analyses (using Rnase/Propidium Iodide staining and flow cytometry) determined G2/M arrest.
   - For the anti-metastatic agent IL-29A, transwell migration/invasion assays, wound healing assays, and EMT marker (E-cadherin and N-cadherin) assessments were performed on metastatic CRC cell lines.

---

## 6. Results

**Bioinformatics Analysis & Candidate Target Discovery:**  
- **Co-expression network analysis (WGCNA) and subsequent clustering** identified modules highly correlated with primary CRC and with liver metastases.
- **Enrichment analysis** of key modules revealed that in primary CRC, cell cycle, p53 signaling, and related processes were upregulated, while in metastatic tumors, pathways related to migration, invasion, and EMT were implicated.
- **Biomarker Identification:**  
  Specific gene signatures were identified for both the primary and metastatic phenotypes. In primary CRC, several genes predicted to regulate cell proliferation were overexpressed. In metastasis-related modules, both upregulated and downregulated genes were noted.

**Drug Screening and Selection:**  
- For primary CRC treatment, two compounds emerged: **Hesperadin** and **BAY-1217389**—both targeting cell cycle regulators such as TTK and NEK2.
- For metastatic CRC, the network suggested that decreased expression of IL10RB (a component of the IL-6/JAK/STAT3 signaling pathway) is associated with metastasis, leading to the exploration of **IL-29A** as an anti-metastatic agent.

**Experimental Validation:**  
- **Anti-Proliferative Effects:**  
  - Hesperadin showed cytotoxic effects in short-term (48-hour) viability assays (with IC₅₀ values around 300–380 nM in HCT-116 and HT-29) and effectively reduced colony formation.
  - BAY-1217389 did not produce strong short-term cytotoxicity but significantly inhibited long-term colony formation.
  - Ki-67 staining confirmed that both agents reduced proliferation and arrested cells in the G2/M phase.
  
- **Anti-Metastatic Effects:**  
  - IL-29A treatment reduced migration and invasion capacities in metastatic CRC cell lines (evidenced by transwell assays and wound healing assays).
  - Immunofluorescence analysis of EMT markers showed that IL-29A increased E-cadherin (epithelial marker) and decreased N-cadherin (mesenchymal marker), suggesting a reversal of EMT processes.

---

## 7. Validations

- **Reproducibility Across Datasets:**  
  The initial gene co-expression modules identified through WGCNA on the training dataset were independently validated on a separate validation dataset, demonstrating consistent module–phenotype associations.
  
- **Network Clustering Metrics:**  
  Multiple network clustering algorithms were used, and their performance was evaluated using internal biological homogeneity indexes and pathway enrichment metrics. This ensured that the selected submodules were robust and biologically meaningful.
  
- **Experimental Confirmation:**  
  The candidate drug effects were validated using standard cell-based assays (WST-1, colony formation, Ki-67 staining, flow cytometry for cell cycle analysis) and migration/invasion assays. The convergence of in silico screening and in vitro functionality strongly supports the therapeutic potential of the selected compounds.

---

## 8. Implications

- **New Therapeutic Avenues:**  
  The integrated approach successfully identifies novel drug targets and suggests treatment alternatives for both primary and metastatic CRC. Specifically, the discovery of compounds like Hesperadin and BAY-1217389 for cell proliferation inhibition, and IL-29A for impeding metastatic processes, could lead to new treatment options.
  
- **Personalized Treatment Strategies:**  
  By distinguishing molecular differences between primary cancers and their metastases, the study supports the development of tailored therapies that address specific pathways in each context.
  
- **Integration of Systems Biology in Drug Discovery:**  
  The work demonstrates how combining transcriptomic data with network-based analyses and drug–target databases can accelerate the identification of actionable targets, ultimately bridging the gap between computational biology and clinical applications.

---

## 9. Clinical Problem Addressed

Metastatic colorectal cancer, particularly liver metastasis, remains difficult to treat effectively. Current therapies—although improving—still fall short in controlling disease progression. This study addresses that clinical problem by:
- Proposing novel therapeutic targets that are specific to the proliferative and metastatic phenotypes observed in CRC.
- Offering candidate compounds (Hesperadin, BAY-1217389, IL-29A) whose mechanisms of action (cell cycle arrest and anti-metastatic effects) directly counteract the identified dysregulated pathways.
- Paving the way for new, potentially more effective and personalized treatment strategies that could ultimately improve patient outcomes in both primary and metastatic colorectal cancer.

---

## In Summary

This paper uses integrated transcriptome and network analyses to identify new treatment alternatives for primary and liver metastatic colorectal cancer. Motivated by the unmet clinical need for effective therapies in metastatic CRC, the study answers the question of how to uncover differential gene modules and candidate biomarkers using co-expression networks (WGCNA) and network clustering, followed by pathway enrichment and drug-target interaction analysis. The study relies on microarray data from multiple GEO datasets and validated these findings on independent datasets. The underlying theories of modular gene co-expression and network pharmacology guide the analysis. The method led to the identification of key biomarkers and associated pathways which, through drug screening on DGIdb, produced candidate therapeutic agents. These candidates were validated in vitro using cell viability, colony formation, proliferation, cell cycle, and migration/invasion assays. The work implies that personalized and more effective therapies for both primary and metastatic CRC can be developed by targeting specific pathways such as cell cycle regulation and EMT. Ultimately, this innovation addresses a critical clinical challenge in treating metastatic colorectal cancer and offers promising new avenues for therapeutic intervention.