# Hypothetical workflow

![[Media/VU B4TM. Hypothetical Workflow 2025-05-28 06.25.41.excalidraw]]


Below is a detailed proposal for a hypothetical study that uses spatial RNA velocity as the primary method to answer a clinically relevant research question—with multiplex immunofluorescence serving as a complementary modality.

---

## Research Question

**Can spatial RNA velocity be used to predict emerging immune‐evasive tumor subpopulations in triple‑negative breast cancer (TNBC), and does integration with multiplex immunofluorescence profiling of the local immune microenvironment improve our ability to forecast response to immunotherapy?**

In other words, the study will address whether measuring the dynamic transcriptional “future state” of tumor cells (via RNA velocity) can reveal regions where cells are transitioning toward more aggressive, immunosuppressive phenotypes—and whether these areas correlate with altered distributions of key immune cell populations (as defined by multiplex IF). Ultimately, this integrated signature could serve as a spatial biomarker for predicting treatment resistance in TNBC patients.

---

## Motivation and Clinical Relevance

Triple‑negative breast cancer is notorious for its aggressive behavior and variable response to immunotherapy. Although many TNBC cases are infiltrated by immune cells, not all patients respond well to immune checkpoint inhibitors. One emerging idea is that tumor cell plasticity—the dynamic ability of tumor cells to change states—can drive the development of immune evasion even before standard markers (such as high PD‑L1 expression or high CD8⁺ T‑cell density) are apparent. By capturing RNA velocity, which uses the ratio of unspliced to spliced transcripts to predict a cell’s future state, this study aims to identify subpopulations of tumor cells in transition toward an immune‑evasive phenotype. By overlaying this with high‑resolution spatial immunophenotyping from multiplex immunofluorescence, we can simultaneously assess “where” these changes occur relative to local immune cells. Such an integrated approach may help refine patient stratification and predict which TNBC patients may ultimately resist immunotherapy.

---

## Data Sources and Acquisition

### Spatial Transcriptomics for RNA Velocity

- **Data Type:**  
  Spatially resolved whole-transcriptome data with information on both spliced and unspliced reads.
  
- **Acquisition Method:**  
  Tissue sections from pre-treatment biopsies or surgical resections of TNBC patients will be processed using a platform capable of capturing both spatial coordinates and RNA velocity information (e.g., an optimized 10× Genomics Visium protocol that preserves unspliced mRNA signals, or Slide-seq V2). This will yield single-cell (or near single-cell) resolution transcriptomics with the necessary kinetic information for RNA velocity analysis.

### Multiplex Immunofluorescence (mIF)

- **Data Type:**  
  High-dimensional protein expression data with single-cell resolution and spatial coordinates.
  
- **Acquisition Method:**  
  An adjacent tissue section (or the same tissue, if compatibility allows) will be stained using a multiplex immunofluorescence panel that includes markers for:
  - Tumor cells (e.g., cytokeratin, SOX10 or Melan-A for distinguishing breast cancer cells)
  - Effector immune cells (e.g., CD8, Granzyme B)
  - Immune regulatory markers (e.g., FOXP3, PD-L1)
  - Stromal cells and other contextual markers (e.g., vimentin for mesenchymal features)
  
  Automated imaging and cell segmentation software (such as inForm or QuPath) will extract cell phenotype, intensity, and precise spatial coordinates.

---

## Theoretical Background

### RNA Velocity Theory

- **Core Concept:**  
  RNA velocity uses the relative abundance of unspliced (nascent) versus spliced (mature) mRNA in each cell to estimate the direction and speed of transcriptional state changes. In a spatial context, mapping these vectors onto tissue architecture provides a “dynamic map” of where tumors are evolving toward different phenotypes, such as a transition toward an immune‑evasive or drug-resistant state.

### Spatial Immune Interactions

- **Concept in TME:**  
  The efficacy of immune responses relies not only on the presence of immune cells but also on their ability to home to, and make contact with, tumor cells. Metrics like nearest-neighbor distances and clustering of immune cells (derived using spatial statistics, e.g., via Weibull models or G-functions) can quantify immune proximity.
  
- **Integration Idea:**  
  By combining RNA velocity (dynamic transcriptional future) with static, yet high-resolution, spatial profiles from mIF, one can explore whether regions where tumor cells are “accelerating” toward an aggressive state are also “immune cold” or conversely, are being robustly infiltrated by effector immune cells.

---

## Proposed Methods and Workflow

### 1. Data Input and Preprocessing

- **Spatial Transcriptomics Processing:**
  - Perform quality control and normalization.
  - Use RNA velocity tools (e.g., scVelo) to compute velocity vectors for each cell by comparing unspliced and spliced transcript counts.
  - Cluster cells into subpopulations based on transcriptional profiles and overlay their velocity vectors on spatial coordinates.
  
- **Multiplex IF Processing:**
  - Segment images to identify single cells and classify them based on integration of multi-channel marker intensities.
  - Extract spatial coordinates and generate a cell-type map.

### 2. Data Integration

- **Spatial Registration:**  
  Align the spatial transcriptomics data and the mIF images using shared tissue landmarks. This step is essential to correlate the transcriptomic “future state” with the spatial distribution of immune cells.

- **Overlay and Spatial Analysis:**
  - Overlay RNA velocity vectors on the mIF cell map.
  - Identify regions where tumor cells show high velocity vectors that may suggest a transition toward an aggressive, immune-evasive state.
  - Quantitatively assess immune cell proximities in these regions (e.g., calculate average nearest-neighbor distances between tumor cells and CD8⁺ T cells, and measure the clustering or exclusion of immune cells).

### 3. Statistical Modeling and Predictive Integration

- **Spatial Metrics:**  
  Calculate spatial metrics (e.g., Weibull parameters of cell-to-cell distances, G-function AUC) for tumor-immune interfaces.
  
- **Integration into a Predictive Model:**  
  Use multivariate regression or machine learning classification (e.g., logistic regression or random forest) to combine the dynamic RNA velocity data (magnitude and direction) with spatial metrics from mIF.  
  - Model output: Predict clinical response to ICI therapy (responder vs. non-responder), recurrence, or progression-free survival.

### 4. Outputs

- **Dynamic Spatial Maps:**  
  Visual representations of tumor sections where RNA velocity vectors are overlaid on immune cell distribution maps. These maps can highlight “hotspots” of anticipated immune evasion.
  
- **Quantitative Biomarkers:**  
  - RNA velocity-based metrics (e.g., average velocity magnitude in critical tumor subregions).
  - Immune proximity metrics from mIF (e.g., mean nearest-neighbor distances, clustering scores).
  - An integrated spatial signature score predictive of immunotherapy outcomes.

- **Predictive Model Outcome:**  
  Statistical output (ROC curves, AUC, sensitivity and specificity values) illustrating how well the integrated biomarker predicts ICI response.

---

## Expected Outcomes and Validation

- **Expected Findings:**  
  Regions where tumor cells exhibit high RNA velocity vectors (indicating rapid state transitions) and a corresponding paucity of infiltrating effector immune cells (as revealed by mIF) would correlate with poor clinical response to ICI.
  
- **Validation Strategies:**
  - **Internal Validation:**  
    Use cross-validation within the same dataset to test model robustness.
  - **External Cohort:**  
    Apply the integrated workflow to an independent cohort of TNBC patients with known outcomes.
  - **Biological Validation:**  
    Confirm that predicted dynamic changes (e.g., markers of stemness or epithelial-to-mesenchymal transition) align with immunohistochemical and molecular profile analyses from adjacent tissue sections.
  - **Clinical Correlation:**  
    Correlate the integrated spatial signature with treatment outcomes (response rates, progression-free survival) in a prospective study.

---

## Implications and Clinical Impact

This integrated study would:
- **Advance Biomarker Discovery:**  
  Provide a refined, dynamic spatial biomarker that captures both cellular state transitions and immune cell interactions.
- **Improve Patient Stratification:**  
  Allow clinicians to identify TNBC patients who may not benefit from ICI therapy due to emerging immune evasion, thereby altering therapeutic decisions.
- **Guide Combination Therapy Development:**  
  Highlight specific tumor regions that may require additional targeted interventions (e.g., combination with agents that modulate tumor cell plasticity) to enhance the efficacy of immunotherapy.
- **Contribute to Understanding Tumor Evolution:**  
  Offer insights into how dynamic changes at the single-cell level influence the broader immune microenvironment, a concept applicable to other cancers as well.

---

In summary, this hypothetical study aims to use spatial RNA velocity as the main tool to discern the future trajectory of tumor cell states in TNBC, with multiplex immunofluorescence providing complementary insights into local immune context. Together, they would address the clinically relevant question of predicting immunotherapy response by offering both dynamic and spatially resolved biomarkers, ultimately contributing to more personalized and effective cancer treatments.

--- 

Below is a detailed proposal for a study design that uses spatial RNA velocity as the primary investigative modality—with multiplex immunofluorescence (mIF) serving as a complementary tool—to predict immunotherapy outcomes. In this hypothetical study, we address a clinically relevant research question and outline how dynamic and spatial features might be merged into an integrated spatial signature score.

---

## Research Question

**Can we predict immunotherapy response in metastatic melanoma by quantifying the dynamic evolution of tumor cell states using spatial RNA velocity and integrating this with local immune spatial metrics from multiplex immunofluorescence?**

In other words, the study aims to determine whether the magnitude and direction of RNA velocity vectors in tumor cells—reflecting their future state trajectories—combined with the spatial distribution and density of key immune cells (e.g., CD8⁺ T cells) can yield a robust integrated signature that predicts which patients will respond favorably to immune checkpoint inhibitors.

---

## Conceptual Overview

### The Role of Spatial RNA Velocity

- **Dynamic Tumor Evolution:**  
  RNA velocity uses the relative abundance of unspliced and spliced mRNA to predict the future transcriptional state of individual cells. When mapped in situ, these vectors reveal which tumor cells are transitioning toward aggressive or immune-evasive phenotypes.
  
- **Interpretation of Magnitude and Direction:**  
  - **Magnitude:** A high velocity magnitude indicates that a cell’s transcriptome is rapidly changing—potentially moving toward a state that might confer resistance or enhanced survival.  
  - **Direction:** If the directional vectors indicate movement toward a signature of immune escape (for example, toward a gene expression profile associated with reduced antigen presentation or increased immunosuppressive signaling), these areas might pinpoint nascent resistant subpopulations.

### The Role of Multiplex Immunofluorescence

- **Spatial Organization of the Immune Microenvironment:**  
  mIF provides high-resolution spatial maps of various cell types. For immunotherapy, the location and proximity of effector immune cells (like CD8⁺ T cells) to tumor cells can determine the likelihood of effective anti-tumor responses.
  
- **Complementing RNA Velocity Data:**  
  While RNA velocity reveals future tumor states, mIF contextualizes these dynamics by showing where immune cells are situated. For example, even if a tumor cell is rapidly evolving toward an immune-evasive state, efficient immune cell trafficking in that region could counterbalance this effect.

---

## Study Design

### Data Inputs

1. **Spatial Transcriptomics Data (for RNA Velocity):**  
   - **Acquisition Method:** Obtain fresh-frozen biopsy specimens from metastatic melanoma patients before initiating immune checkpoint inhibitor therapy.  
   - **Platform:** Use a spatial transcriptomics technology (e.g., an optimized 10× Genomics Visium protocol or Slide‑seq V2) that preserves both unspliced and spliced mRNA counts at near/single-cell resolution along with precise spatial coordinates.
   - **Output:** Gene expression matrices along with spatial coordinates and computed RNA velocity vectors (each with magnitude and directional information).

2. **Multiplex Immunofluorescence Data (for Spatial Immune Profiling):**  
   - **Acquisition Method:** Process an adjacent tissue section (or, where possible, use a combined protocol compatible with the spatial transcriptomics assay) with a panel of antibodies (e.g., CD8, PD-1, Granzyme B, FOXP3, Melan-A, and other lineage markers).  
   - **Output:** High-resolution images with segmented single cells, their phenotypic classifications, and spatial coordinates.

---

### Data Processing Workflow

1. **Preprocessing and RNA Velocity Calculation:**  
   - **Quality Control:** Filter out low-quality cells/spots and normalize the spatial transcriptomics data.  
   - **Velocity Computation:** Use tools such as scVelo to calculate RNA velocity vectors for each cell; these vectors will yield for each cell a magnitude (indicative of the rate of transcriptional change) and a direction (indicating the predicted future expression state).

2. **Clustering and Defining Tumor Cell Subpopulations:**  
   - Cluster tumor cells based on their transcriptomic profiles.  
   - Identify subpopulations that are transitioning toward aggressive or immune‑evasive states through RNA velocity analysis (e.g., by visualizing where many vectors converge toward a distinct state).

3. **Processing mIF Data:**  
   - **Cell Segmentation and Phenotyping:** Use image analysis software (like QuPath or inForm) to segment the mIF images, classify cells into tumor vs. immune subtypes, and extract their coordinates.
   - **Spatial Metric Calculation:** Calculate spatial statistics such as:
     - The average nearest-neighbor distance between CD8⁺ T cells and tumor cells.
     - Density metrics of immune cells within tumor microdomains.
     - Clustering indices that describe how tightly immune cells are aggregated around tumor regions.

4. **Data Integration – Registering the Datasets:**  
   - Align the spatial transcriptomics and mIF datasets using tissue landmarks or morphological features, ensuring that RNA velocity vectors can be overlaid on the corresponding immune cell spatial maps.

5. **Feature Extraction for the Integrated Signature:**

   - **From Spatial RNA Velocity:**
     - **Average Velocity Magnitude:** Compute the mean velocity magnitude within regions of interest (ROIs) or along tumor borders.
     - **Directional Consistency:** Quantify the predominant vector directions in these ROIs, possibly scoring the degree to which they align with an “immune-escape axis” as defined by known gene signatures.
   
   - **From mIF Spatial Metrics:**
     - **Immune Proximity Score:** Calculate metrics such as the inverse of the average distance between CD8⁺ T cells and nearby tumor cells.
     - **Infiltration Density:** Quantify the density of cytotoxic immune cells within defined tumor regions.

6. **Integrated Spatial Signature Score Calculation:**
   - **Normalization:** Convert each feature (e.g., velocity magnitude, directional alignment, immune proximity, immune density) into normalized scores (such as z-scores) to ensure comparability.
   - **Weighted Combination:**  
     - Define a composite score (S) as a weighted sum (or product) of these normalized features:
       \[
       S = w_1 \times V + w_2 \times D + w_3 \times P + w_4 \times I
       \]
       where:
       - \(V\) represents the normalized average RNA velocity magnitude (higher values may indicate rapid change toward aggressive states),
       - \(D\) represents the normalized directional consistency (e.g., toward an immune‑evasive profile),
       - \(P\) represents the normalized immune proximity score (lower distances—i.e. higher scores—indicate effective immune infiltration),
       - \(I\) represents the normalized immune cell density,
       - \(w_1,w_2,w_3,w_4\) are weights derived from either a training dataset using logistic regression (or another multivariate method) or expert biological knowledge.
   
   - **Interpretation:**  
     - A high integrated spatial signature score might characterize regions where fast-evolving tumor cells (high \(V\) and \(D\)) are poorly surveilled (low \(P\) and \(I\)), predicting poor immunotherapy response.
     - Conversely, a lower score might indicate stable tumor cells or effective immune engagement.

7. **Predictive Modeling and Validation:**
   - Use the integrated score as an input to logistic regression or machine learning classifiers to predict clinical outcomes (e.g., response vs. non-response).
   - Validate the model using cross-validation and, if available, an independent patient cohort.

---

## Expected Outputs

- **Spatial Maps:**  
  Visualizations that overlay RNA velocity vectors on immunofluorescence-derived immune cell maps, highlighting “hotspots” of dynamic tumor evolution relative to immune surveillance.
  
- **Quantitative Biomarkers:**  
  A set of normalized spatial metrics derived from both RNA velocity and mIF, along with the final integrated spatial signature score.
  
- **Predictive Model Performance Metrics:**  
  ROC curves, AUC values, sensitivity, specificity, and predictive accuracies of the integrated signature in forecasting response to immunotherapy.

- **Biological Insights:**  
  Correlations between high integrated spatial signature scores and poorer patient outcomes, providing mechanistic insight into how emerging immuno-evasive tumor subpopulations affect therapy response.

---

## Summary of Integration Approach

1. **Extract Dynamic Data:**  
   Quantify the RNA velocity magnitude and direction for individual tumor cells to capture their future state trajectories.

2. **Extract Spatial Data:**  
   From mIF images, calculate metrics describing the distribution of immune cells around tumor cells (such as nearest-neighbor distances and cell densities).

3. **Combine Metrics:**  
   Normalize and weigh these dynamic and spatial features to generate a composite integrated spatial signature score predictive of immunotherapy outcomes.

4. **Validate Predictively:**  
   Use statistical and machine learning models to establish the correlation between the composite score and clinical outcomes, thereby providing a holistic biomarker that informs treatment decisions.

---

## Clinical Impact

If successful, this integrated approach can:
- Identify early "danger zones" in tumors where rapid cell state transitions occur in the absence of effective immune surveillance.
- Provide clinicians with spatially resolved biomarkers that improve patient stratification for immunotherapy.
- Advance personalized therapy by enabling targeted interventions in regions of the tumor most likely to drive resistance.

This study leverages the cutting-edge capability of spatial RNA velocity to capture tumor cell dynamics, complemented by the precise spatial resolution of mIF, to yield a multifaceted and clinically relevant predictive biomarker for immunotherapy response.