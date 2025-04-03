# Biologically Informed Neural Networks Predict Drug Responses

[Beyond the black box with biologically informed neural networks](Biology/Seminars/Beyond%20the%20black%20box%20with%20biologically%20informed%20neural%20networks.md)
[paper link](https://www.cell.com/cancer-cell/fulltext/S1535-6108(20)30488-8?_returnURL=https%3A%2F%2Flinkinghub.elsevier.com%2Fretrieve%2Fpii%2FS1535610820304888%3Fshowall%3Dtrue)

The paper presents **DrugCell**, a biologically informed neural network model designed to predict the responses of cancer cells to drug treatments, including monotherapies and drug combinations.

---

## What are their motivation?

- Predicting and understanding drug response in cancer
- Many different features can lead to drug response prediction. Many DL methods using these features do not offer biological insight.
	- What if we just use traditional ML? Like ASCA?
- BINN approaches:
	- use prior knowledge or data to add structure to the model, which can then be interpreted
		- example: a study mapped _raw molecular measurements_ to a set of pre-defined _metabolic pathways_ drawn from prior knowledge bases; the _states_ of these pathways predict antibiotic resistance in E. Coli., with particular pathway features emerging as _candidate mechanisms of resistance_
	- post-hoc analysis of weights and features
		- weights assigned to each input gene by a black-box neural network model are subjected to gene set enrichment analysis to identify pathways regulating drug response

## What Did They Do?

- Developed **DCell**: a visible neural network (VNN) to simulate yeast
- Mapping the neurons of a DNN into a large _hierarchy_ of known and putative _molecular components and pathways_
- DCell _predicts_ mutation impact on cellular growth response and _identify_ the most relevant pathways driving those predictions
- Building from DCell, developed **DrugCell**, a VNN that simulates the response of cancer cells to drugs.
- Uses the hierarchical structure of human cell biology, allowing for response predictions for any drug in any cancer and intelligent design of effective combination therapies.
- The key innovation was embedding **biological insights**, specifically from the Gene Ontology (GO) database, into the neural network design to increase model interpretability without sacrificing predictive accuracy.

---

## What Question Did They Answer?

1. Can a neural network informed by biological hierarchies predict drug responses with high accuracy?
2. Can the model’s outputs be interpreted mechanistically to understand biological pathways mediating drug sensitivity or resistance?
3. Can this approach guide effective drug combination designs and improve clinical outcomes?

---

## What Theories Did They Use?

1. **Gene Ontology (GO)**: DrugCell's architecture reflects the hierarchical nature of biological processes in human cells, with neurons structured to mirror known relationships between cellular subsystems (e.g., pathways, complexes).
2. **Visible Neural Networks (VNNs)**: This paradigm links neural network layers to biological processes, allowing direct mapping between inputs (mutations) and specific biological subsystems to enhance interpretability.
3. **Drug Structure Representation**: A separate artificial neural network (ANN) branch models the drug's chemical structure using Morgan fingerprints, which are canonical vector representations of molecular structures.

---

## How Did They Develop and Use the Biologically Informed Neural Network?

1. **Network Design**:
   - **Two Branches**:
     - The **genotype branch** is a VNN with neurons hierarchically organized based on GO subsystems (e.g., glycolysis, MAPK signaling). This branch predicts the cell's functional state based on its genotype (mutation status). -> genotype embedding
     - The **drug branch** is a conventional ANN that encodes the drug's molecular structure using Morgan fingerprints. -> drug embedding
   - These branches are integrated in a final layer to predict drug response.

2. **Training**:
   - The model was trained using data from 1,235 tumor cell lines and 684 drugs, covering all major tissue types.
   - The data link cell line genotypes to dose-response curves (AUC values) across drugs.
   - Training incorporated mutation information (binary vectors for 3,008 genes) and drug fingerprint data, covering major tissue and drug types.

3. **Interpretability**:
   - The hierarchical design allowed the authors to connect predicted drug responses to specific biological pathways or subsystems.
   - They ranked pathways using a metric called RLIPP (Relative Local Improvement in Predictive Power), which identifies the most critical subsystems driving drug response predictions.

4. **Applications**:
   - Predictions were validated by experimental data, such as CRISPR/Cas9 combinatorial gene editing and drug synergy screens.
   - The model was used to propose effective drug combinations, which were experimentally tested in cell lines and PDX models.

---

## What Outcomes Did They Get?

1. **Predictive Accuracy**:
   - DrugCell achieved strong predictive performance (Spearman correlation of 0.80 in cross-validation), comparable to black-box models.
   - It maintained interpretability without sacrificing accuracy.

2. **Mechanistic Insights**:
   - Plotted the first 2 principal components of genotype and drug embeddings; shows separation between genotypes known to confer specific drug sensitivities?
      - they do not show the % variance explained in their PCA plots
      - and not very strong separation seen in the plot
      - it's normal that a NN can learn to separate them if they are important predictors for drug response. You can probably use a deep enough random forest or just a regular FC NN to capture those.
   - The model identified specific pathways mediating drug responses, including metabolic pathways modulating sensitivity to chemotherapy agents like paclitaxel.
   - CRISPR validation supported the biological relevance of top-ranked pathways.

Questionable statement: Since DrugCell's VNN is structured according to the hierarchy of biological subsystems comprising a human cell, its output (genotype embedding) is the result of state changes in particular subsystems within that hierarchy.

3. **Drug Combination Design**:
   - DrugCell successfully predicted synergistic drug combinations based on the parallel pathway inhibition theory. For example:
     - Combination of paclitaxel with a glycolysis inhibitor enhanced efficacy.
     - A PI3K inhibitor combined with an ERK pathway inhibitor extended survival in PDX models.

4. **Clinical Validation**:
   - Its predictions were validated across various systems, including experimental drug sensitivity screens, combinatorial CRISPR studies, and patient-derived xenograft (PDX) models.
   - In patient-derived xenografts (PDX) and metastatic breast cancer patient data, DrugCell predictions stratified sensitive and resistant cases, improving progression-free survival outcomes.

---

## What Are the Implications?

1. **Increased Interpretability**:
   - DrugCell demonstrates that embedding biological knowledge into machine learning models enables mechanistic insights, bridging the gap between "black-box" AI and human understanding of biological systems.

2. **Guiding Precision Medicine**:
   - The model can inform personalized treatment by predicting drug sensitivity based on patient-specific tumor genotypes.

3. **Designing Drug Combinations**:
   - The ability to rank biological pathways opens avenues for rational design of combination therapies, reducing trial-and-error in drug development.

4. **Future Applications**:
   - DrugCell provides a framework for biologically informed modeling in other domains, such as rare diseases or non-cancer pathologies where training data are limited.
