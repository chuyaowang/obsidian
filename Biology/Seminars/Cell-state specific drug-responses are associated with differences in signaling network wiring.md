# Cell-state specific drug-responses are associated with differences in signaling network wiring

#paper 
[link](https://www.biorxiv.org/content/10.1101/2025.01.27.635060v1.full)
## 1. Motivation

**Why They Did It:**  

The study is driven by the longstanding puzzle of why isogenic cells—cells with the same genetic background—can respond so differently to the same drug treatment. In many cases, such heterogeneous responses underlie drug tolerance or resistance in diseases like cancer. The authors aim to decode how intrinsic differences between cells (their “cell-states”) influence the wiring of intracellular signaling networks and, ultimately, determine how these cells _respond_ when key signaling pathways (like those triggered by Epidermal Growth Factor, EGF) are _inhibited_. In essence, they want to know whether the cell's pre-existing state alters the flow of signals in a way that impacts drug efficacy and whether this can be modeled at single-cell resolution.

---

## 2. The Research Question

**Core Inquiry:**  
The paper asks:  
*How do cell-state–dependent differences in signaling network wiring affect the response to targeted pharmacological inhibition?*  

More specifically, the study seeks to answer whether and how the “wiring” or quantitative strength of interactions between phospho-proteins within the EGF receptor network differs between various cell-states—and if these differences explain why some cells respond differently to the same drug.

---

## 3. Relevant Theories and Their Explanations

### Wiring of Signaling Networks:

The study is rooted in the idea that cellular signaling is not a simple linear cascade but rather a complex, interconnected network of interactions. In these networks, the “wiring”—that is, which proteins interact and with what strength—determines how signals are processed. Differences in network wiring can alter the cell’s response even if the same upstream signal is received.

### Feedback Loops and Cross-Talk:

Many signaling pathways (e.g., MAPK and Akt-mTOR) include built-in feedback loops and cross-talk between pathways. Such designs ensure robustness and adaptability but also create opportunities for differential drug responses. For instance, inhibition of one kinase might lead to compensatory activation elsewhere.

### Cell-State Heterogeneity:

Even within a uniform population, cells can reside in distinct “states” influenced by factors such as the cell cycle, differentiation status, and prior signaling events. The concept is that these intrinsic states affect the arrangement and function of signaling networks—so that the same drug can have markedly different effects across subpopulations.

### EGF stimulation

  EGF (Epidermal Growth Factor) stimulation is a classic method to trigger a cascade of intracellular signaling events. When EGF binds to its receptor (EGFR) on the cell surface, it causes receptor dimerization and autophosphorylation. This activation initiates multiple downstream signaling pathways, including the MAPK/ERK and the PI3K/Akt-mTOR cascades. These pathways subsequently:
	- **Activate Phosphorylation Cascades:** For example, the phosphorylation of ribosomal protein S6 (RPS6) is a well-known downstream event that reflects the active state of these pathways.  
	- **Modulate Cellular Functions:** The activated signaling network leads to changes in gene expression, alters cell-cycle progression, and influences processes such as proliferation, differentiation, and survival.  
	- **Facilitate Signal Cross-talk:** EGF stimulation not only activates its immediate downstream targets but also provokes alterations in signaling from other pathways via cross-talk (e.g., effects on JNK, p38, and Wnt pathways).

In the study, applying EGF after a period of growth without it served to provoke a controlled activation of the cells' signaling machinery, allowing the researchers to capture the phosphorylation dynamics that indicate how the network processes external cues.

Together, these theories suggest that to fully understand and predict drug responses, one must consider not only the identity of network components but also their dynamic interconnections as determined by a cell’s state.

---

## 4. Methods

**Experimental Design:**

- **Cell System and Treatments:**  
  The authors worked with primary human epidermal keratinocytes (karyotypically normal cells) to avoid confounding genetic mutations. They subjected these cells to an EGF stimulation in combination with targeted drug treatments using inhibitors of two key downstream effectors:
  - **p90RSK Inhibitor (BI-D1870)**: inhibits Erk/MAPK
  - **p70S6K Inhibitor (PF4708671)**: inhibits Akt/mTOR
  
- **Single-Cell Protein Profiling (scID-seq):**  
  They employed single-cell ImmunoDetection-by-sequencing (scID-seq) to measure ~69 (phospho-)proteins per cell. This high-dimensional data allowed them to capture both signaling activity and cell-state information.

> [!info]- Why phospho protein only
> **Phosphorylation as a Direct Readout:**
> 
> - **Signal Transduction Core:** Phosphorylation is the fundamental mechanism through which intracellular signals are transmitted. Many proteins switch between active and inactive forms based on their phosphorylation status. By focusing on these modifications, the study directly captures the active state of key signaling players.
>   
> - **Rapid and Reversible Dynamics:** Phosphorylation events are rapid and reversible, making them excellent markers for transient signaling events. This is key when studying the immediate effects of stimuli (like EGF) or drug treatments on a cell.
>   
> - **Mapping Network Wiring:** Because the intracellular signaling network is built upon interactions mediated by kinase activities (e.g., activation of downstream effectors like ERK1/2 or Akt), only a subset of total proteins—the phosphorylated fraction—is relevant for reconstructing and quantifying the exact wiring and strength of these interactions.
> 
> Thus, by measuring phospho-proteins, the researchers were able to effectively profile the dynamic state of the signaling network, which is essential for understanding how different cells respond to external stimuli and targeted perturbations.

> [!info]- Why samples are pooled
> 
> 1. **What Samples Were Pooled?**  
>    The authors pooled together cells coming from different treatment groups. In their experiment, these samples included the various conditions they applied—such as cells treated with p90RSK inhibitors, cells treated with p70S6K inhibitors, and the vehicle control. Before pooling, each of these groups had been uniquely barcoded (using cell-hashing) so that when they are combined, the origin of each cell (i.e., its treatment condition) can still be identified later.
> 
> 2. **What Do “Plates” Refer To?**  
>    In this context, "plates" are the 96-well plates used in the workflow. After the pooled samples were stained with the full panel of antibodies, individual cells were then sorted by Fluorescence-Activated Cell Sorting (FACS) into the wells of these 96-well plates. Each well typically serves as a separate, small reaction vessel, which is especially useful for downstream processes like library preparation in single-cell sequencing experiments.
> 
> 3. **Why Are the Samples Pooled?**  
>    Pooling the samples serves a few key purposes:
>    - **Randomization and Minimization of Batch Effects:** By combining the different treatment groups and then distributing them randomly across the 96-well plates, the authors ensure that any variation due to independent sample preparation or staining is evenly spread across all groups. This reduces the risk that observed differences are simply due to technical variation.
>    - **Efficiency in Processing:** Pooling all samples before staining with the full antibody panel allows for a uniform and simultaneous treatment, making downstream processing and comparisons more straightforward.
>    - **Consistent Staining:** It minimizes variation in staining efficiencies between the different conditions since all cells receive the same antibody treatment in one combined step.
> 
> In summary, the authors pooled together all the differently treated cell samples (barcoded to retain treatment identity) to be stained in a single, uniform process. Then, by sorting individual cells into 96-well plates via FACS, they randomized the treatment groups over the independent sample preparations done per plate, thus controlling for technical variation and enhancing the reliability of the downstream single-cell analysis.

- **Cell-State Identification:**  
  By selecting a subset of 23 proteins that were relatively unresponsive to drug treatments as “cell-state markers” and applying robust clustering algorithms (using UMAP for dimensionality reduction and a consensus-based Leiden algorithm), they defined nine distinct cell-state clusters.

> [!info]- Why unaffected proteins as cell state markers
> **Rationale Behind “Cell-State Markers”:**
> 
> - **Stability Across Perturbations:** Proteins that remain relatively unaltered by acute drug treatment represent intrinsic properties of the cells (such as differentiation status, cell-cycle stage, or basal metabolic state). They provide a stable snapshot of the cell’s baseline condition.
>   
> - **Minimizing Confounding Effects:** By selecting these stable markers, the researchers avoided confusing the inherent cell-state (i.e., the pre-existing, internal condition of the cell) with the transient, treatment-induced changes. This distinction is crucial when trying to correlate inherent cell heterogeneity with differential drug responses.
>   
> - **Defining Intrinsic Cellular Heterogeneity:** Clustering based solely on these “cell-state markers” allows the identification of distinct cell populations that exist before any treatment is applied. Later on, the researchers can link these intrinsic states to how each subpopulation responds to the drugs.
>   
> - **Reliable Classification:** Using proteins that are insensitive to treatment ensures that the cell grouping or clustering isn’t distorted by the perturbation itself, but rather reflects meaningful differences in the biology of individual cells.
> 
> In essence, these markers are used as a control or baseline to tease apart whether the observed differences in drug responses are due to inherent cell-state differences rather than just direct effects of the drugs on protein phosphorylation levels.

- **Computational Network Reconstruction (scCNR):**  
  To quantify the strengths of interactions between nodes (phospho-proteins) in the signaling network, the authors developed and applied a single-cell Comparative Network Reconstruction (scCNR) method. This model uses the natural variation in signaling protein levels across single cells to determine how changes in one protein’s activity affect others, with the ability to detect differences in wiring between cell states.

> [!info]- How scCNR works
> ### What scCNR Does
> **scCNR (single-cell Comparative Network Reconstruction)** is an algorithm designed to reconstruct and compare the wiring of intracellular signaling networks across different cell states using single-cell phospho-protein data. It lets researchers quantify how strongly each protein (node) in the network influences another and, crucially, how these interaction strengths differ between cell states.
> 
> - **Reconstructs Network Interactions:**  
>   scCNR takes quantitative measurements of phospho-protein levels obtained from thousands of individual cells. It assumes that the natural cell-to-cell variability (or “noise”) in these measurements acts as a series of subtle perturbations. By observing how the fluctuations in one protein correlate with those in another, the algorithm infers the underlying interaction strengths between signaling proteins.
>   
> - **Quantifies Interaction Strengths:**  
>   Each edge in the network is assigned an interaction strength \( r_{ij} \), defined as the percent change in the activity of node \( i \) given a 1% change in node \( j \)’s activity, assuming all other nodes are held constant. This provides a quantitative measure of how much influence one protein exerts over another.
>   
> - **Compares Networks Across Cell States:**  
>   scCNR is designed to reconstruct networks for different cell populations (or cell states) while keeping the overall topology—i.e., which proteins are connected—constant. It then allows the interaction strengths (the weights on the edges) to vary between these states. This comparison highlights which interactions are modulated by intrinsic cell-state differences or treatment effects (such as drug responses).
> 
> ---
> 
> ### How the Algorithm Works
> 
> 1. **Input and Prior Information:**  
>    - **Data Input:** The primary input is single-cell phospho-protein measurements. These measurements capture the dynamics of signaling pathways (often after a stimulus like EGF or a drug perturbation).
>    - **Topology Initialization:** Optionally, you can incorporate prior knowledge about the network’s structure—for example, which proteins are known to interact (from literature or databases). This helps initialize the model with a canonical topology.
> 
> 2. **Mathematical Framework:**
>    - **Estimating \( r_{ij} \):**  
>      For any pair of proteins (nodes) \( i \) and \( j \), scCNR estimates the relative influence \( r_{ij} \) based on the covariance of their activities across cells. In essence, it models the effect of a 1% change in node \( j \)’s activity on node \( i \)’s activity.
>    - **Regression/Optimization:**  
>      The algorithm uses an optimization framework (similar in spirit to penalized regression) in which it fits the network model to the observed data. It finds the set of edge weights that best explains the variations in protein abundance across cells.
> 
> 3. **Penalizing Complexity:**
>    - **Balancing Fit vs. Complexity:**  
>      To avoid overfitting, scCNR employs a penalty on the number of interactions (edges) included in the network. This favors a simpler model that adequately explains the data.
>    - **Cell-State Specific Differences:**  
>      In comparing multiple cell states, scCNR adds an extra penalty for differences in edge strengths between states. This forces the algorithm to only select differences that meaningfully improve the overall model fit, thus highlighting the most relevant changes in network wiring.
> 
> 4. **Statistical Validation:**
>    - **Bootstrapping and Permutations:**  
>      The robustness of the inferred interactions is assessed using bootstrapping (resampling the single-cell data repeatedly) and permutation tests (randomizing cell-state assignments). These steps help determine which differences are statistically significant and not due to random fluctuations.
>    - **Model Comparison:**  
>      The algorithm’s performance is measured by metrics such as the root mean square of residuals (RMSR), and its outcome is compared to randomly generated models to confirm that the reconstructed network is both robust and significantly better than chance.
> 
> 5. **Output:**  
>    - **Edge Weights for Each Cell State:**  
>      The final output is a set of network interaction strengths for each defined cell state. This allows researchers to see, for example, that one cell state might have a stronger coupling between a receptor and a downstream kinase compared to another state.
>    - **Identification of Key Differences:**  
>      By comparing networks across conditions, scCNR pinpoints which interactions are modulated in a cell-state–dependent manner—a key insight for understanding differential drug responses.
> 
> ---
> 
> ### In Summary
> 
> - **Purpose:** scCNR leverages the natural variability in single-cell data to reconstruct signaling networks and to identify how interaction strengths differ between cell states.
> - **Mechanism:** By modeling the percent change in one protein relative to another (under a predefined or inferred network structure), it quantifies edge strengths and uses penalized optimization to prevent overfitting and to highlight significant differences.
> - **Outcome:** Researchers obtain a quantitative, cell-state–specific view of signaling network wiring, which can elucidate mechanisms of drug resistance, variation in cellular responses, and potentially guide therapeutic strategies.
> 
> Would you like to learn more details about potential extensions of this method—such as integrating additional omics layers—or discuss how this approach might be tailored to specific disease models?
> 
> - **Additional Analyses:**  
>   They also used linear regression models, machine learning classifiers, and permutation tests to statistically assess differences in drug responses and network wiring across cell states, and complemented the protein data with single-cell RNA sequencing to link signaling changes with transcriptional outputs.

---

## 5. Results

**Major Findings:**

- **Drug Effects Propagate Across the Network:**  
  Inhibition of p90RSK and p70S6K reduced phosphorylation of their immediate targets (e.g., RPS6) but also led to pronounced changes in other parts of the signaling network. For example, blocking p90RSK led to accumulated ERK1/2 phosphorylation—likely due to negative feedback loops—while p70S6K inhibition altered components in the JNK, p38, and Wnt pathways.

- **Cell-State Determines Drug-Response:**  
  The study found that the impact of drug treatment (e.g., changes in the abundance of cyclins or histone phosphorylation) varied significantly across the nine distinct cell-state clusters. Some cell states exhibited unique responses that were not seen as strongly in others, indicating a strong cell-state dependency.

- **Differential Network Wiring:**  
  Using scCNR, the authors identified a subset of interactions (“edges”) between phospho-proteins that exhibited significant differences in strength across cell states. Out of the modeled interactions, 31 edges were particularly critical, and 22 of these showed statistically significant cell-state–specific differences. This demonstrates that the intrinsic wiring of the signaling network can vary and correlate with differential drug responses.

- **Transcriptional Consequences:**  
  Changes in kinase activity and pathway cross-talk were linked with altered transcription factor profiles (e.g., c-JUN and Myc), suggesting that the rewiring of the signaling network feeds forward into changes in gene expression.

---

## 6. Validation

**How They Confirmed Their Findings:**

- **Reproducibility Using Alternative Inhibitors:**  
  The researchers validated key observations—especially those involving transcriptional changes—using an independent p90RSK inhibitor, confirming that the effects were not compound-specific.

- **Robust Clustering Approaches:**  
  They employed a consensus clustering strategy that repeated the Leiden algorithm 1,000 times with a “majority vote” system to ensure stable identification of the nine cell states. Machine learning classifiers (logistic regression, random forests, SVM) further validated that the signaling markers could predict cell-state identity.

- **Model Robustness (scCNR):**  
  For the network reconstruction, the authors compared their model performance (in terms of the root mean square of residuals) against 1,000 randomly generated models and performed bootstrapping experiments and permutation analyses. These approaches confirmed that the identified edges were statistically robust and not due to random chance.

---

## 7. Implications

**What Does It Mean?**  
- **For Basic Science:**  
  The paper reinforces the notion that the internal wiring of the signaling network is not static but is intimately linked to the cell’s state. This means that even within a homogeneous cell population, the network architecture can differ, leading to diverse responses to the same stimulus.

- **For Clinical Strategies:**  
  Given that many targeted therapies (especially in cancer) aim at specific kinases, understanding that drug effects can propagate in unexpected ways—and that these effects may be cell-state dependent—has direct implications. It suggests that therapeutic strategies should account for signaling network heterogeneity. Optimally, a multi-targeted or combination therapy approach might be necessary to overcome intrinsic drug resistance driven by cell-state variability.

---

## 8. Clinical Problems Addressed

**How the Innovation Helps Clinically:**  
The study’s insights are particularly relevant for overcoming drug resistance in cancer treatment. Tumors are known to be heterogeneous, and a subpopulation of cells may harbor a distinct signaling network wiring that renders them less sensitive to a given drug. By identifying cell-state–specific wiring differences and the propagation effects of targeted inhibitors, the work sheds light on why some cancer cells evade treatment. Ultimately, these findings could contribute to the design of more sophisticated treatment regimens that simultaneously target multiple nodes or feedback loops in the network, thereby reducing the chance of resistance and improving patient outcomes.

---

## In Conclusion

This paper makes a significant contribution by showing that:
- Intracellular signaling network wiring is not uniform but tailored by the cell’s state.
- Drug responses are heavily modulated by these intrinsic differences.
- A robust combination of single-cell proteomics and advanced computational modeling (scCNR) can unravel these complex interdependencies.

The study not only deepens our understanding of cellular signaling but also has important implications for designing strategies to combat drug resistance in clinical settings, particularly in cancer therapies where heterogeneity is a major challenge.