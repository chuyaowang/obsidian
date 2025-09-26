# Functional enrichment of alternative splicing events with NEASE reveals insights into tissue identity and diseases

#paper 
[link](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-021-02538-1)

## 1. Motivation

The study is driven by the challenge of understanding the functional consequences of alternative splicing (AS) events. Although AS dramatically increases transcript diversity and plays a major role in tissue identity, development, and disease, its precise functional impact—especially at the protein and interaction level—remains poorly understood. Existing methods typically take a gene-level approach (for example, standard gene set enrichment analyses), which treats all AS-affected genes equally and overlooks the possibility that only a subset of AS events (those that alter protein features like domains and motifs) truly impact cellular function. To overcome this gap, the authors introduce NEASE—a tool designed to “enrich” AS events by integrating structural annotations of protein–protein interactions into a systems-based view of the interactome.

---

## 2. Research Question

The key question the paper addresses is:  
**How can we systematically characterize the functional consequences of alternative splicing events by directly focusing on changes in protein features and their mediated interactions?**

In other words, rather than simply cataloging which genes are differentially spliced, the study asks how AS-driven alterations in protein structure (e.g., loss or gain of domains, motifs, or residues) translate into changes—or “edgetic” alterations—in the protein–protein interaction network. This aims to reveal pathways and mechanisms that contribute to tissue identity and disease.

---

## 3. Relevant Background Information

The study builds on several pieces of background information:

- **Alternative Splicing and Transcript Diversity:**  
  AS is a crucial mechanism that expands the repertoire of RNA and protein isoforms in human cells. It is known to contribute to cell type specification and to be deregulated in various diseases, including cardiomyopathy, muscular dystrophy, and autoimmune disorders. However, because not every splicing event results in a functional change at the protein level (some might be neutral or even represent splicing noise), a more nuanced analysis is essential.

> [!info]- How are alternative splicing events detected
> In this study, alternative splicing (AS) events are detected by leveraging RNA sequencing (RNA-seq) data and then applying specialized computational tools and resources that quantify and characterize splicing changes. Here’s a detailed breakdown of the process:
> 
> 1. **RNA-seq as the Data Source:**  
>    The primary data type is RNA-seq, which provides high-throughput, quantitative measurements of transcript abundance across different tissues and conditions. RNA-seq captures reads that span exon–exon junctions as well as reads aligning fully within exons, offering clues about which exons are included or skipped in the mature transcript.
> 
> 2. **Quantification of Splicing – PSI Values:**  
>    One common metric derived from RNA-seq is the Percent Spliced In (PSI) value for an exon. PSI quantifies the proportion of transcripts in which a particular exon is retained relative to the total (retained plus skipped). By comparing PSI values across different samples or conditions, the researchers can pinpoint exons whose inclusion levels vary significantly—indicative of alternative splicing events.
> 
> 3. **Specialized Software Tools:**  
>    The study makes use of published tools designed for AS detection:
>    - **MAJIQ, rMATS, and Whippet:** These tools analyze RNA-seq alignments (typically based on reads that map to splice junctions or exonic regions) to detect and quantify various types of AS events, such as exon skipping, alternative 5’ or 3’ splice sites, mutually exclusive exons, and intron retention.
>    - Such tools take the raw RNA-seq data (after alignment to a reference genome) and generate lists or tables of AS events—with associated statistics (e.g., changes in PSI values and significance measures)—which highlight exons that are differentially included between sample groups.
> 
> 4. **Integration with Curated Databases:**  
>    In addition to directly processing the RNA-seq data, the study also leverages resources like VastDB and GTEx:
>    - **VastDB:** This is a curated database that has already quantified multiple types of AS events from a wide array of RNA-seq samples across different tissues and developmental stages. It provides readily comparable PSI values and splicing event annotations.
>    - **GTEx:** Similarly, GTEx offers a comprehensive atlas of tissue-specific gene expression and, more recently, splicing information. These resources help validate and contextualize the splicing events detected in the experiments.
> 
> 5. **Mapping to Protein Features:**  
>    Once the AS events are detected and quantified (e.g., via differential PSI values), the study maps the coordinates of these alternatively spliced exons to protein features using structural databases such as Pfam. This step is critical because it helps distinguish which AS events are likely to affect protein domains, motifs, or residues (and consequently protein–protein interactions), rather than representing splicing noise.
> 
> 6. **Downstream Analysis with NEASE:**  
>    With a set of AS events in hand—particularly those affecting protein features—the NEASE tool then integrates this information with a joint structural network of protein–protein interactions (PPIs), domain–domain interactions (DDIs), and domain-motif interactions (DMIs). This network-based view allows the authors to focus on “edgetic” changes (i.e., changes in interactions mediated by specific protein features due to AS).
> 
> ---
> 
> **In Summary:**  
> - **Detection:** RNA-seq data is processed using dedicated splicing detection tools (e.g., MAJIQ, rMATS, Whippet) to identify and quantify alternative splicing events by measuring changes in PSI values.
> - **Validation and Contextualization:** The detected events are cross-referenced with large-scale databases like VastDB and GTEx, ensuring that only robust, tissue-specific, or condition-specific splicing variations are considered.
> - **Structural Mapping:** Exon coordinates are mapped onto protein features (domains, motifs, residues) to determine the potential functional impact of the splicing events.
> - **Application in NEASE:** Only events with likely functional consequences (i.e., those affecting protein structure and interactions) are carried forward into the NEASE analysis, which then interrogates the impact of AS on cellular pathways.
> 
> This multi-step approach—from raw RNA-seq to protein-focused AS analysis—ensures that the study detects alternative splicing events accurately and associates them with functional biological outcomes.

- **Traditional Functional Enrichment Approaches:**  
  Typically, researchers perform gene set enrichment analyses on lists of differentially spliced genes. This approach, however, ignores whether the splicing events alter protein structural domains or interaction motifs. Such changes, when they occur, can rewire the protein–protein interaction (PPI) network, influencing cellular processes.

- **Limitations of Existing Tools:**  
  Several tools exist for isoform- or exon-level analysis (like IsoformSwitchAnalyzeR, tappAS, and DIGGER), but they generally do not provide a systematic, network-based functional interpretation that links AS events to specific biological pathways.

The background thus sets up the need for a tool that not only detects AS events but also interprets their potential biological impact by considering how they alter PPIs and pathway connectivity.

---

## 4. Relevant Theories

Several theories underlie the NEASE approach:

- **Edgetic Perturbation Theory:**  
  This concept suggests that disease and altered cellular phenotypes may result not from a wholesale loss or gain of entire proteins, but rather from specific changes in their interaction “edges.” In the context of AS, a splicing event might remove or modify a protein domain, thereby impairing certain PPIs while leaving others intact. NEASE taps into this idea by focusing on the “edges” in the interaction network that are affected by splicing.

- **Network-Based Enrichment in Systems Biology:**  
  Traditional enrichment analyses consider discrete lists of genes, but network-based approaches consider relationships among genes (or, here, protein features). By incorporating structural annotations (e.g., from Pfam) together with known protein–protein and domain–domain interactions, the NEASE method leverages the topology of biological networks to identify which pathways are most impacted by AS events.

- **Statistical Overrepresentation Analysis:**  
  NEASE uses a hypergeometric test—but importantly, it applies that test at the level of interaction edges rather than genes. Additionally, a weighted NEASE score is introduced to de-emphasize hub proteins that may otherwise lead to false positives.

Together these theories support a more refined, interaction-centric approach to understand functional changes due to alternative splicing.

---

## 5. Method

The NEASE method proceeds through several steps:

1. **Mapping AS Events to Protein Features:**  
   - Exons from AS events are annotated using structural databases like **Pfam** to determine which protein domains, motifs, or residues they encode. This exon-centric mapping helps to focus on those splicing events likely to have functional impact. Exon - domain

2. **Constructing a Joint Structural Interaction Network:**  
   - The authors integrate a standard protein–protein interaction (PPI) network (e.g., from BioGRID) with protein–protein interface data such as domain–domain interactions (from databases like DOMINE and 3did), domain–motif interactions (from ELM), and structural information from the Protein Data Bank (PDB). This creates a “joint graph” that connects protein features to the interactions they mediate. Domain-structure-interation

3. **Identifying Affected Edges:**  
   - Using the exon-to-feature mapping, NEASE determines which interaction edges in the _joint network_ would be disrupted or altered by the observed AS events.

4. **Edge-Level Enrichment Analysis:**  
   - Instead of considering changes in genes, NEASE performs a one-sided hypergeometric test on the set of affected network edges to test for overrepresentation in biological pathways curated from databases (via ConsensusPathDB and others). It calculates both unadjusted p values and a weighted “NEASE score” that penalizes hub nodes.

> [!info]- Hypergeometric test and NEASE score
> The hypergeometric test is a statistical method that evaluates the probability of drawing a specific number of “successes” from a finite population without replacement, assuming a random sampling process. In other words, it answers the question: "Given a total population divided into two groups (e.g., items belonging to a specific pathway and those that don’t), what is the likelihood of observing a particular number (or more) of items from the pathway within a selected subset?"
> 
> ### How the Hypergeometric Test Works
> 
> Imagine you have a deck of cards where a fixed number are aces. If you draw several cards randomly (without putting them back), the hypergeometric distribution tells you the probability of drawing a certain number of aces. Formally, if:
> - \( N \) is the total number of items (e.g., all edges in the entire interactome),
> - \( K \) is the total number of items that are “successes” (e.g., the number of edges that are known to belong to a particular biological pathway),
> - \( n \) is the number of items drawn (e.g., all the edges that are affected by alternative splicing events),
> - \( k \) is the number of successes in your drawn sample (e.g., the count of affected edges that also belong to the pathway),
> 
> then the probability of drawing exactly \( k \) successes is calculated with the hypergeometric probability mass function. When testing for overrepresentation, we usually calculate the p value as the probability of observing \( k \) or more successes, assuming there’s no enrichment.
> 
> ### How It’s Used in This Study
> 
> In the NEASE framework, the authors are not simply counting differentially spliced genes; instead, they focus on how alternative splicing (AS) events perturb the protein interaction network at the level of individual edges. Here’s how the hypergeometric test comes into play:
> 
> 1. **Defining the “Population”:**  
>    The total population (\( N \)) is the set of all protein interactions (edges) in the structurally annotated, joint interactome.
> 
> 2. **Successes in the Population:**  
>    The successes (\( K \)) are the subset of those edges that belong to a particular biological pathway (for example, the “Muscle Contraction” pathway).
> 
> 3. **Defining the Sample:**  
>    The sample (\( n \)) comprises the edges that are “affected” by alternative splicing events—that is, edges whose mediating protein domains or motifs are altered due to splicing.
> 
> 4. **Counting the Overlap:**  
>    Within this set of affected edges, \( k \) represents the number of edges that are part of the pathway under investigation.
> 
> The one-sided hypergeometric test then calculates the p value—the probability that one would observe at least \( k \) affected edges in the pathway if the AS events had impacted edges uniformly at random. A very low p value indicates that the enrichment of affected edges in that pathway is unlikely to have occurred by chance, thus suggesting that the pathway is significantly impacted by AS.
> 
> ### The NEASE Score
> 
> The NEASE method builds on this edge-level enrichment analysis. In addition to reporting p values from the hypergeometric test, NEASE introduces a weighted score (the “NEASE score”) that combines:
> - The p value (reflecting the statistical significance of the enrichment), and
> - The number of significant spliced genes that contribute affected interactions toward the pathway.
> 
> This additional weighting is designed to penalize highly connected hub proteins, which may naturally have many interactions by chance but are less informative about specific functional shifts. By down-weighting those hubs, the NEASE score prioritizes pathways where the enrichment is driven by a larger number of distinct genes with altered interactions. In other words, the NEASE score provides a ranking or overall measure of how robust and biologically meaningful the enrichment is.
> 
> ### How to Interpret the P Value and NEASE Score
> 
> - **P Value Interpretation:**  
>   If the p value is very low (for instance, \( p < 0.001 \)), it suggests that the number of AS-affected edges falling into a given pathway is much higher than what we would expect if splicing events were distributed randomly across the interactome. This indicates significant enrichment and implicates the pathway as potentially functionally impacted by AS.
> 
> - **NEASE Score Interpretation:**  
>   The NEASE score combines the significance of the p value with the breadth of gene involvement. A higher NEASE score (or a better ranking when comparing scores across pathways) means that not only is there significant enrichment (i.e., very unlikely to occur by chance), but also that the enrichment is driven by many spliced genes. This helps to prioritize pathways that are more likely to be biologically relevant and highlights candidate biomarkers or targets for further investigation.
> 
> ### In Summary
> 
> - **Hypergeometric Test:** Used to determine the probability that the number of AS-affected interactions in a specific pathway occurs by chance.
> - **P Value:** A low p value indicates that the observed enrichment of affected interactions is statistically significant, suggesting a true impact of alternative splicing on that pathway.
> - **NEASE Score:** A composite metric that adjusts the p value by taking into account the number of genes contributing to the enrichment, with penalties for hub proteins. This score helps to rank pathways based on both statistical significance and the breadth of splicing impact.
> 
> Together, these measures allow NEASE to provide a nuanced, network-level interpretation of the functional consequences of alternative splicing, facilitating the discovery of pathways and candidate biomarkers that are functionally perturbed in a tissue- or disease-specific manner.

5. **Prioritization and Visualization:**  
   - NEASE can then prioritize specific genes and pathways that show a significant number of affected interactions, offering insights into potential biomarkers or mechanistic alterations. An interactive Python package supports deeper analysis and visualization.

The method is applied in several use cases, including tissue-specific splicing in neural and muscle tissues, differences between reticulated and mature platelets, and splicing alterations in multiple sclerosis and dilated cardiomyopathy.

---

## 6. Key Results

- **Tissue Identity and Function:**  
  Analysis of tissue-specific exons (from VastDB) revealed distinct clusters of exons in neural versus muscle/heart tissues. NEASE successfully linked these subsets to relevant pathways—the neural exons were enriched in synaptic vesicle cycle and neurotransmission-related pathways, while muscle-specific exons were enriched in muscle contraction pathways. Interestingly, NEASE delivered more biologically meaningful insights than classical gene-level enrichment.

- **Platelet Function:**  
  In the comparison of reticulated (young) versus mature platelets, NEASE identified significant enrichment of GPCR downstream signaling and other platelet activation pathways. This finding aligns with the known prothrombotic phenotype and high signaling activity in reticulated platelets, providing evidence that AS plays a role in platelet function.

- **Disease Applications:**  
  In multiple sclerosis, NEASE identified splicing-related pathways related to neurotransmitter receptor signaling, MAPK cascades, and even links with immune processes. Similarly, in dilated cardiomyopathy, NEASE detected affected interactions that correspond to key disease pathways, underscoring the potential of the tool in uncovering splicing biomarkers in complex disease settings.

---

## 7. Validation

The robustness of NEASE is validated through multiple approaches:

- **Comparison with Gene-Level Enrichment:**  
  In several case studies, NEASE is contrasted with classic gene-level overrepresentation analyses. In many instances, NEASE outperforms gene-level methods by capturing the specific protein interaction changes due to AS, leading to higher ranking and significance for biologically relevant pathways.

- **Network Comparison and Permutation Tests:**  
  The authors compare the structurally annotated joint network against the full PPI network to demonstrate that their filtered network does not overly bias results toward hub proteins. Permutation tests further support the statistical robustness of the enrichment p values produced by NEASE.

- **Cross-Dataset Confirmation:**  
  The authors corroborated tissue-specific splicing results by comparing PSI values from VastDB and GTEx, confirming that the AS events driving the enrichment are indeed highly upregulated in the expected tissues.

These validations lend confidence that NEASE not only finds statistically significant results but also delivers biologically interpretable and robust insights.

---

## 8. Implications

The innovations presented by NEASE have several significant implications:

- **Enhanced Functional Interpretation of AS:**  
  By shifting the focus from gene-level changes to edge-level perturbations in the interactome, NEASE provides unique insights into how AS can rewire cellular networks. This perspective helps reveal mechanistic details that might be overlooked by classical methods.

- **Biomarker Discovery:**  
  The tool’s ability to highlight new candidate genes and pathways affected by AS could lead to the identification of novel biomarkers for diseases. For example, in multiple sclerosis or cardiomyopathy, the method points to specific splicing events that may serve as diagnostic or prognostic markers.

- **Complementary Approach in Systems Biology:**  
  NEASE serves as a complementary tool to existing transcriptomic and proteomic analyses by adding a layer of structural and network-based information. This integrated view is likely to improve our understanding of tissue identity, development, and disease etiology, potentially informing new therapeutic strategies.

---

## 9. Clinical Problems Addressed

NEASE directly addresses the clinical and biomedical challenge of deciphering the functional impact of aberrant splicing, which is implicated in many diseases:

- **Neurological Diseases:**  
  In conditions such as multiple sclerosis, where AS could contribute to the dysregulation of neuronal signaling and immune responses, NEASE offers a mechanism for uncovering which splicing events are functionally relevant. This may lead to improved biomarkers or even targets for splicing-modulation therapies.

- **Cardiomyopathy:**  
  Alternative splicing is also implicated in the pathogenesis of dilated cardiomyopathy. By pinpointing specific splicing events that alter key signaling pathways in the heart, NEASE could help identify targets for therapeutic intervention or aid in patient stratification.

- **Platelet Disorders and Hemostasis:**  
  The study of reticulated versus mature platelets using NEASE highlights its potential in understanding and eventually treating disorders related to platelet activation and thrombosis.

By providing a nuanced, network-level interpretation of splicing events, NEASE helps bridge the gap between high-throughput splicing data and actionable clinical insights, ultimately contributing to personalized medicine strategies in diverse fields—from neurology to cardiology and hemostasis.

---

## In Summary

The paper introduces NEASE, a novel network-based enrichment tool designed to functionally annotate alternative splicing events by focusing on the protein features and interactions they affect. Motivated by the inadequacy of gene-level enrichment methods to capture the nuanced impact of AS, the authors address how splicing events can rewire protein–protein interactions and thereby influence key biological pathways. By integrating structural annotations with PPIs and applying a rigorous edge-level enrichment analysis, NEASE delivers robust insights across several applications—ranging from tissue identity in neural and muscle cells to disease contexts like multiple sclerosis and dilated cardiomyopathy. The tool not only validates its findings against classic analyses and permutation tests but also highlights its potential to uncover new biomarkers and therapeutic targets, ultimately addressing clinically relevant challenges associated with splicing dysregulation.
