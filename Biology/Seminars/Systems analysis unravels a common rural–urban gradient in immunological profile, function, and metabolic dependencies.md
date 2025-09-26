# Systems analysis unravels a common rural–urban gradient in immunological profile, function, and metabolic dependencies

#paper 
[link](https://www.science.org/doi/10.1126/sciadv.adu0419)

---
## Motivation  

Urbanization alters environmental exposures and lifestyle, driving profound shifts in human immunity. Rural populations often show vaccine hyporesponsiveness and heightened inflammatory signatures, yet most immunological studies focus on affluent, urban cohorts. The authors aim to dissect how the immune system remodels along the rural-to-urban continuum in understudied regions, leveraging a multi-omics systems approach to link cell composition, functional responses, metabolic state and antibody glycosylation.

---

## Research Question  

How does the human immune system vary continuously from rural to urban settings, and which cellular, functional, metabolic and molecular features define this gradient?  

---

## Background  

- Environmental drivers of immune variation include chronic infections (e.g., CMV), “trained immunity” from microbial components, diet and lifestyle factors.  
- Prior work showed rural African cohorts display heightened immune activation, altered IgG glycosylation and skewed cytokine profiles.  
- Integrative, multi-cohort single-cell analyses are needed to capture population-level immune remodeling without erasing genuine biological differences.

### Data Types & Acquisition  

1. **Cohorts**  
   - 37 age- and sex-matched adults:  
     * Rural Senegalese (RUR SEN)  
     * Urban Senegalese (URB SEN)  
     * Urban Dutch (URB NLD)  
   - Validation cohort: independent Indonesian rural–urban samples.  

2. **Assays**  
   - **Mass cytometry** (EXV): deep immunophenotyping of PBMC subsets.  
   - **Spectral flow cytometry** (MET): metabolic enzyme expression in ex vivo PBMCs.  
   - **Functional stimulation**: PMA/ionomycin and MPL (TLR4 agonist) assays, cytokine readouts.  
   - **IgG Fc glycosylation**: LC-MS profiling of serum antibodies.  
   - **CITE-seq**: paired single-cell transcriptome and surface-protein profiling on PBMCs.  

3. **Metadata**  
   - Socioeconomic and environmental surveys (household size, animal contact, flooring).  
   - Schistosomiasis status via circulating anodic antigen assay.  

---

## Relevant Theories  

- **Multi-Omics Factor Analysis (MOFA):** Unsupervised latent factor model that captures axes of variation shared across heterogeneous datasets.  
- **Principal Curve Analysis:** Nonlinear trajectory fitting through high-dimensional data to order samples along a continuous gradient.  
- **Trained Immunity:** Epigenetic/metabolic reprogramming of innate cells by prior exposures, modulating subsequent responses.  
- **Batch Correction vs. Biology Preservation:** Techniques to align datasets without removing true biological signals.

---

## Methodology  

1. **Data Integration**  
   - Applied MOFA on five datasets (EXV, MET, PMA, MPL, GLY) to learn latent factors associated with rural-urban status.  
   - Used PERMANOVA on MOFA factors to quantify separation of cohorts.  

2. **Trajectory Inference**  
   - Fitted a principal curve on MOFA embeddings, assigning each individual a continuous **λ** score reflecting their position along the rural–urban axis.  

3. **Differential Abundance & Functional Analyses**  
   - Performed cluster-level differential abundance tests on mass- and spectral-cytometry data to identify cell subsets enriched along the gradient.  
   - Measured cytokine production in key subsets under PMA/ionomycin and MPL stimulations.  
   - Assessed metabolic enzyme levels (e.g., ACC1, G6PD, cytochrome c) within those subsets.  

4. **IgG Glycosylation Correlation**  
   - Quantified Fc glycoforms (galactosylation, fucosylation, sialylation) and correlated them with frequencies of proinflammatory B cells.  

5. **Single-Cell Validation (CITE-seq)**  
   - Mapped identified clusters in RNA+ADT space to confirm marker expression, transcriptional programs and metabolic gene signatures.  

6. **Metabolic Perturbation**  
   - Treated PBMCs with inhibitors of glycolysis, pentose phosphate pathway and fatty acid synthesis prior to stimulation to probe substrate dependencies of cytokine responses.  

---

## Results  

- **Continuous Immune Gradient:** MOFA factors 1–3 and principal curve λ scores increased monotonically from rural Senegalese → urban Senegalese → urban Dutch.  
- **B Cell Remodeling:**  
  - Rural settings enriched for CD11c⁺ proinflammatory B cells producing TNF.  
  - These CD11c⁺ B cells showed upregulated ACC1 (↑ fatty acid synthesis) and downregulated cytochrome c (↓ oxidative phosphorylation).  
  - Altered IgG Fc glycosylation in rural individuals (↑ fucosylation, ↓ galactosylation) correlated with CD11c⁺ B cell frequencies.  

- **NK Cell Adaptation:**  
  - Rural cohorts had higher frequencies of adaptive (NKG2C⁺) NK cells with low CD122/CD161 expression and attenuated IFN-γ responses to MPL—consistent with reduced accessory cytokine sensitivity.  

- **T Cell Shifts:**  
  - Enrichment of CD161⁺ CD4⁺ T subsets in rural individuals, exhibiting higher TNF and IFN-γ production and elevated G6PD levels (↑ pentose phosphate activity).  
  - Transcriptional upregulation of interferon-stimulated genes (IFIT3, IFI44L) in CD161⁺ CD4⁺ T cells.  

- **Monocyte Activation:**  
  - Rural monocytes displayed higher baseline HLA-DR and spontaneous TNF secretion in resting culture.  
  - Upon stimulation, they produced more proinflammatory cytokines and relied differentially on glycolysis and PPP.  

- **Metabolic Dependencies:**  
  - Glycolysis inhibition reduced TNF responses most in urban samples, while FAS and PPP blockade disproportionately impaired rural cytokine outputs—revealing distinct energy wiring across the gradient.  

- **Cross-Cohort Validation:**  
  - Core signatures (e.g., CD11c⁺ B cell enrichment, altered glycosylation, adaptive NK expansion) recapitulated in an independent Indonesian rural–urban cohort.  

> [!note]- Differential analyses still done in original space
> Differential analyses (for example, finding “differentially expressed” genes or “differentially abundant” cell subsets) are **not** done directly on the MOFA latent factors themselves, but rather in the **original feature spaces**, with the MOFA factors used to guide and contextualize those downstream tests. Concretely, the paper’s pipeline works like this:
> 
> 1.  Fit MOFA to all of the assays to learn a shared, denoised latent representation (the matrix Z of factors) and feature loadings (the matrices $W^{(v)}$ that summarize how each original feature (cell‐subset frequency, enzyme abundance, glycoform, gene or protein) contributes to each factor.
> 
> 2.  Use the latent factors Z (and in particular the “rural–urban” trajectory λ derived from Z) as a continuous covariate to  
>     a.  **Rank or select** features whose original measurements correlate most strongly with the trajectory, or  
>     b.  **Adjust for confounders**—e.g. include the top MOFA factors as covariates in a regression to remove technical variation before testing.
> 
> 3.  **Perform the statistical tests** (trend tests, ANOVA, linear models, nonparametric correlations) directly on the **original measurements** for each feature:  
>     – For mass-cytometry clusters, test whether the raw cluster frequencies differ along λ.  
>     – For glycoforms, test whether the LC-MS intensities covary with λ.  
>     – For CITE-seq genes or ADT counts, use standard single-cell DE tools (e.g. MAST, edgeR) with λ or MOFA factors included as covariates.
> 
> 4.  **Interpretation via loadings:** to understand which genes underlie a given latent factor, you can also inspect its loading vector W^(v) in the transcriptomic view: features with the highest absolute weights are the ones driving that axis.
> 
> In short, MOFA’s VB inference and ARD priors give you  
>   • a compact, batch-corrected embedding of each sample (Z),  
>   • per-view loading matrices (W) that tell you which original features load onto each factor, and  
>   • a way to impute missing modalities.  
> 
> But **all “differential” calls**—“which clusters go up or down from rural to urban?” or “which genes are up in CD11c⁺ B cells?”—are done back in the **original feature spaces**, using the MOFA factors/trajectory only to prioritize, covary out noise, or assign samples to positions along a continuum.

> [!note]- Reconstructed matrix for denoising
> When you see the paper testing “differential abundance” or “differential expression” of features in the original measurement space, it looks like they’re simply comparing raw counts or frequencies—but in fact **all of that testing is done on MOFA‐*denoised* data or *with* batch/technical factors explicitly accounted for**, so the unwanted variation doesn’t sneak back in.  Here’s how they avoid reintroducing batch effects:
> 
> 1.  **MOFA as a Batch‐Corrector**  
>     - MOFA doesn’t just give you sample embeddings \(Z\) and feature loadings \(W\); it also provides a **reconstruction** of each view:  
>       $$
>         \hat X^{(v)} \;=\; W^{(v)}\,Z
>       $$ 
>     - That reconstructed $\hat X^{(v)}$ is effectively a **denoised, batch‐corrected** version of the original $\,X^{(v)}$.  
>     - All downstream tests for “which clusters go up or down” or “which glycoforms correlate” are performed on those $\hat X^{(v)}$ values, not on the raw data.
> 
> 2.  **Including MOFA Factors as Covariates**  
>     - When they do statistical trend tests or ANOVAs on the *original* measurements (e.g. cluster frequencies, enzyme levels, glycan abundances), they always include the **top MOFA factors** (or the continuous rural–urban trajectory λ) as covariates in their linear models.  
>     - Any variation that MOFA assigned to technical or batch factors is thus statistically “soaked up” and doesn’t confound the group comparisons.
> 
> 3.  **Validation That MOFA Didn’t Over‐correct**  
>     - They show that the MOFA factors that they’re using for correction or covariates are the *same* factors that correlate with biology (rural–urban status) and *not* with instrument or cohort labels.  
>     - PERMANOVA on the MOFA space confirms that the largest axes of variation map to rural/urban differences, *not* to batch or site effects.
> 
> 4.  **Subset‐Specific Analyses**  
>     - Within each assay, all samples were processed together (same panel, same instrument run), or were randomized across batches where possible.  So any residual batch effects are orthogonal to the comparisons of interest.  
>     - For the small CITE‐seq subset, they reprocessed the data in a single joint pipeline.
> 
> Taken together, these design and analysis choices mean that—even though the final statistical tests “live” in the original measurement space—the data have been effectively batch-corrected by MOFA (and, where needed, by including MOFA latent dimensions as covariates).  The comparisons you see in Figs. 3–6 are therefore **biological** differences, not technical artifacts.

---

## Key Figures and Tables  

| Figure / Table | Description                                                                                                     |
|--------------|-----------------------------------------------------------------------------------------------------------------|
| Fig. 1       | Cohort demographics and IgG1 Fc galactosylation levels across RUR SEN, URB SEN, URB NLD.                        |
| Fig. 2       | (A) Schematic of assays; (B) MOFA variance explained; (C) MDS separation; (D) Principal curve trajectory; (E–F) Correlation of λ with key immune features. |
| Fig. 3       | (A) UMAP of B cell subsets; (B–C) Heatmaps of differentially abundant clusters in EXV/MPL; (D–E) TNF production and metabolic enzymes in CD11c⁺ B cells; (F) IgG glycoform–B cell correlations; (G–I) CITE-seq validation of CD11c⁺ B cell signature. |
| Fig. 4       | NK cell landscape: EXV/PMA/MPL cluster heatmaps; (E–G) NKG2C⁺ frequencies, functional assays, CMV status; (H–L) CITE-seq adaptive NK features. |
| Fig. 5       | CD4⁺ T cell trajectories: UMAP clusters (EXV/PMA); heatmaps of cluster abundances; cytokine and enzyme levels in CD161⁺ subsets; CITE-seq gene/protein markers. |
| Fig. 6       | Monocyte cluster analyses (EXV/PMA/MPL); baseline TNF secretion; HLA-DR correlation; G6PD levels; CITE-seq subset markers. |
| Table S1–S4 | Participant metadata, assay summaries, cluster marker definitions and statistical test results.                   |

---

## Validation  

- **Statistical Tests:** Trend tests, ANOVA with Tukey correction, PERMANOVA for multivariate separation, FDR control.  
- **Functional Confirmation:** Independent Indonesian cohort reproduced core signatures.  
- **Schistosomiasis Control:** No major impact of low-intensity infection on identified immune features.  
- **CITE-seq Cross-Validation:** Single-cell transcriptome and surface‐protein data confirmed mass- and spectral-cytometry–derived clusters and metabolic gene programs.  

---

## Implications  

- Reveals a **shared immunological trajectory** across ancestries and geographies as populations urbanize.  
- Identifies **cell-type–specific metabolic rewiring** underlying functional differences, informing targeted immunomodulation.  
- Highlights the interplay between **antibody glycosylation** and B cell activation in rural settings.  

---

## Clinical Problem Addressed  

By pinpointing how rural environments foster proinflammatory, metabolically rewired immune states and dampen vaccine responsiveness, this work:  

- Provides biomarkers (CD11c⁺ B cells, adaptive NK expansion, glycoforms) to **predict vaccine efficacy** in LMIC settings.  
- Suggests metabolic or adjuvant interventions (e.g., modulating FAS or PPP) to **enhance vaccine immunogenicity** among rural populations.  
- Enables tailored strategies for **disease prevention and immunotherapy** in communities undergoing rapid urbanization.

---

## Data integration challenges

The study integrates five distinct assays across multiple populations to reveal a continuous rural–urban immune trajectory. This ambitious scope raises several critical integration challenges, which the authors tackle as follows:

### 1. Heterogeneous Data Modalities  
- Assays span cytometry (mass and spectral flow), functional cytokine readouts, glycomics (IgG Fc–glycan profiling) and transcriptomic/protein data (CITE-seq).  
- Each modality produces different feature types (cell frequencies, enzyme expression levels, cytokine percentages, glycoform abundances, RNA/ADT counts) with distinct scales and noise profiles.  
- **Solution:** Multi-Omics Factor Analysis (MOFA) learns a shared latent space that aligns these heterogeneous features without manual normalization or feature engineering.

### 2. Batch Effects across Platforms and Sites  
- Samples come from three geographic cohorts (rural Senegalese, urban Senegalese, urban Dutch) assayed on separate days, instruments and operators.  
- Platform-specific biases (e.g., differences in antibody panels or instrument sensitivity) can overshadow genuine biological variation.  
- **Solution:** MOFA’s factorization model inherently partitioned technical variance (batch) from biological signals, capturing rural–urban differences in top latent factors while minimizing platform artifacts.

### 3. Disparate Feature Dimensionalities  
- Datasets range from ~60 cytometry clusters to dozens of glycoforms and thousands of transcriptomic/protein measurements.  
- Direct concatenation would overweight high-dimensional assays.  
- **Solution:** MOFA imposes per-dataset view weights and learns dataset-specific loadings, ensuring each assay contributes appropriately to joint factors.

### 4. Missing Data and Assay Subsets  
- Not every individual was profiled by every assay (e.g., only a subset underwent CITE-seq).  
- Standard integration methods often require complete data matrices.  
- **Solution:** MOFA handles missing entries natively, estimating latent factors from available views without discarding partially profiled samples.

### 5. Preserving Biological Heterogeneity  
- Aggressive batch correction risks erasing real immunological differences (e.g., cell-type shifts driven by urbanization).  
- **Solution:** The authors validated that MOFA factors correlated with known biological markers (IgG glycosylation, eosinophil counts) and not simply batch labels, then used principal-curve ordering on latent space to recover a biologically meaningful rural-urban continuum.

### 6. Cross-Population Validation  
- Ensuring the integrated model generalizes beyond the discovery cohorts to other ancestries and geographies.  
- **Solution:** Core signatures derived from MOFA (e.g., CD11c⁺ B cell enrichment) were validated in an independent Indonesian rural–urban cohort and by mapping CITE-seq data onto the same latent factors, confirming robustness across populations and modalities.

---

By addressing these challenges—heterogeneous modalities, batch effects, missing data, feature imbalance and cross-population generalizability—the paper demonstrates a scalable pipeline for multi-omic, multi-cohort integration of immune profiles.

## MOFA

MOFA (Multi-Omics Factor Analysis) is an unsupervised latent-factor framework designed to integrate heterogeneous omics datasets measured on the same samples. It uncovers a low-dimensional representation—“factors”—that capture the principal axes of variation shared across assays or unique to individual views.

---

### Model Overview  

MOFA models each omics view $v$ (e.g., mass cytometry, glycomics, transcriptomics) as a linear combination of $K$ latent factors plus view-specific noise:

$$
\mathbf{X}^{(v)} = \mathbf{W}^{(v)} \mathbf{Z} + \mathbf{E}^{(v)}
$$

- $\mathbf{X}^{(v)}\in\mathbb{R}^{D_v\times N}$: data matrix for view $v$ (features × samples)  
- $\mathbf{Z}\in\mathbb{R}^{K\times N}$: shared factor matrix (latent factors × samples)  
- $\mathbf{W}^{(v)}\in\mathbb{R}^{D_v\times K}$: weight/loading matrix linking factors to features  
- $\mathbf{E}^{(v)}$: residual noise, assumed Gaussian  

Each sample $n$ obtains a $K$-dimensional embedding in $\mathbf{Z}_{:,n}$, summarizing its multi-omic profile.

---

### Capturing Shared and View-Specific Variation  

To allow factors to explain only a subset of views, MOFA imposes **sparsity priors** on loadings:

- **Automatic relevance determination (ARD)** priors on each column of $\mathbf{W}^{(v)}$  
- A factor $k$ with near-zero loadings across all features in view $v$ is effectively “turned off” for that view  

This yields factors that can be:  
- **Shared** across multiple assays  
- **Specific** to a single omics modality  

> [!note]- ARD
> #### Purpose of ARD  
> 
> Automatic Relevance Determination is a Bayesian mechanism for selecting which latent factors truly explain variation in each data view. It lets the model automatically “turn off” factors that are irrelevant to a particular omics modality without manual feature selection.
> 
> #### How ARD Works  
> 
> Each latent factor $k$ has an associated **precision** (inverse variance) hyperparameter $\alpha_{v,k}$ for view $v$. The loading of feature $d$ on factor $k$ in view $v$, denoted $w^{(v)}_{d,k}$, is assumed to follow a zero-mean Gaussian prior:
> 
> $$
> p\bigl(w^{(v)}_{d,k}\,\big|\,\alpha_{v,k}\bigr)
> = \mathcal{N}\bigl(0,\;\alpha_{v,k}^{-1}\bigr).
> $$
> 
> A **large** value of $\alpha_{v,k}$ forces $w^{(v)}_{d,k}$ to shrink toward zero, effectively silencing factor $k$ in view $v$. A **small** $\alpha_{v,k}$ allows nonzero loadings, marking the factor as relevant.
> 
> #### Determination of ARD Hyperparameters  
> 
> - Each $\alpha_{v,k}$ is itself given a conjugate Gamma prior:  
>   $\alpha_{v,k}\sim \mathrm{Gamma}(a_0,b_0)$.  
> - During variational-Bayes inference, the model jointly optimizes:  
>   - Factor loadings $w^{(v)}_{d,k}$  
>   - Latent factors $z_{k,n}$  
>   - Precision hyperparameters $\alpha_{v,k}$  
> - The update for $\alpha_{v,k}$ balances (a) its prior and (b) the aggregate squared magnitude of its loadings. If most $w^{(v)}_{\ast,k}$ remain small, $\alpha_{v,k}$ grows, shutting down that factor for view $v$.
> 
> #### Effect in MOFA  
> 
> - **Shared factors** have low $\alpha_{v,k}$ across many views, contributing to multiple omics layers.  
> - **View-specific factors** maintain low $\alpha$ in just one dataset and high $\alpha$ elsewhere.  
> - Thus ARD yields interpretable factors automatically tagged as global or modality-specific, enhancing both integration and biological insight.

---

### Handling Missing Data  

MOFA natively accommodates missing entries by treating them as latent variables. During inference, it:  
- Marginalizes out missing observations in the likelihood  
- Learns factors from available data only  
- Retains samples profiled in only a subset of views  

---

### Inference via Variational Bayes  

Exact posterior inference is intractable, so MOFA uses a **variational Bayesian** approximation:

1. **Define a mean-field variational family** over $\mathbf{W}^{(v)}$,$\mathbf{Z}$, and ARD precision hyperparameters  
2. **Optimize the evidence lower bound (ELBO)** with respect to variational parameters  
3. **Iterate until convergence**, yielding posterior means for factors and loadings  

This yields an approximate posterior $q(\mathbf{Z},\{\mathbf{W}^{(v)}\})$ that captures uncertainty.

> [!note]- Purpose of this step
> 
> The variational-Bayes (VB) step in MOFA serves a single, crucial purpose: to approximate the intractable posterior distribution over the model’s latent variables (the factors Z, the view-specific loadings W, and the ARD precision hyperparameters) in a way that is both computationally efficient and scalable to high-dimensional, multi-view data.  
> 
> #### Why Exact Inference Is Intractable  
> 
> MOFA’s probabilistic model defines a joint distribution  
>   $$p(X, Z, {W^{(v)}}, \alpha)$$  
> over all data views X, latent factors Z, factor-to-feature loadings $W^{(v)}$, and precision hyperparameters α (which govern sparsity). Computing the true posterior  
>   $$p(Z, {W^{(v)}}, \alpha | X)$$
> requires integrating over an enormous continuous parameter space—something we cannot do in closed form for realistic datasets.
> 
> #### Goal of Variational Bayes  
> 
> VB turns inference into optimization. We posit a simpler, factorized “variational” distribution  
>   $q(Z, {W^{(v)}}, α)$ 
> and then adjust its free parameters to make q as close as possible to the true posterior. Concretely, VB maximizes the **Evidence Lower BOund** (ELBO):  
>   $ELBO(q) = E_q[log p(X, Z, {W}, α)] – E_q[log q(Z, {W}, α)]$ 
> Maximizing this lower-bounds the true log-marginal likelihood log p(X), ensuring that q captures the dominant modes of the true posterior.
> 
> #### Outputs of VB in MOFA  
> 
> Once the ELBO converges, VB gives us:  
> - **Posterior means of Z**: the K-dimensional embeddings of each sample in factor space  
> - **Posterior means of W^(v)**: the loadings showing how strongly each feature in view v contributes to each factor  
> - **Precision hyperparameters α**: which drive the ARD sparsity, effectively turning factors “on” or “off” in each view  
> 
> #### Why This Matters  
> 
> - **Scalability**: VB scales to thousands of samples and features, whereas exact methods would blow up.  
> - **Handling Missing Views**: Because q is optimized with only observed entries, VB naturally accommodates samples missing entire data modalities.  
> - **Uncertainty Quantification**: The variational posterior provides not just point estimates but also uncertainty (via posterior variances) for downstream analyses.  
> - **Interpretable Latents**: VB learns a compact, denoised representation (the Z’s and W’s) that drives the multi-omic integration and trajectory inference.
> 
> In short, the VB inference in MOFA lets us turn a complex probabilistic model of heterogeneous omics into concrete, efficiently computable sample embeddings and feature loadings that capture the shared—and view-specific—axes of biological variation.

---

### Interpretation of Outputs  

- **Factors ($\mathbf{Z}$)**: Coordinates of samples in latent space  
  - Visualize via PCA or UMAP to identify sample groupings (e.g., rural vs. urban)  
  - Correlate factors with external phenotypes (e.g., lambda trajectory)  

- **Loadings ($\mathbf{W}^{(v)}$)**: Feature contributions to each factor  
  - High absolute weight indicates strong association  
  - Enables identification of marker features driving shared or assay-specific variation  

- **Variance Decomposition**: For each factor and view, MOFA computes the fraction of variance explained, revealing which assays contribute most to each axis of variation.

---

### Advantages of MOFA  

- Integrates **heterogeneous data types** without manual normalization  
- Discerns **shared vs. unique** signals across omics layers  
- Handles **partial sample profiles** gracefully  
- Yields **interpretable axes of variation** that can be linked to biological or clinical covariates  

By transforming multi-view data into a concise set of interpretable factors, MOFA enables downstream analyses—trajectory inference, clustering, correlation with covariates—on a unified, denoised latent space.

## Integrating with scPoli

[Population-level integration of single-cell datasets enables multi-scale analysis across samples](Biology/Seminars/Population-level%20integration%20of%20single-cell%20datasets%20enables%20multi-scale%20analysis%20across%20samples.md)

Here’s how the conditional-VAE strategy behind scPoli could be grafted onto the rural–urban immune study to sharpen its integration, interpretation and extensibility:

1.  Embed Samples and Cells Jointly  
    • In scPoli, each sample (here: each donor/cohort) gets a fixed-size “condition” embedding, and each cell (or cell-subset profile) gets a latent vector that’s learned in the context of its sample.  
    • Replace—or augment—MOFA’s continuous factors with a CVAE that conditions on sample covariates (rural vs. urban, geography, infection status) to learn:  
      – A low-dimensional sample embedding capturing technical + environmental differences.  
      – A cell-level latent code capturing the multi-omic state (phenotype, metabolism, cytokine response).  
    • Benefit: you recover a disentangled representation where batch effects (instrument, site) live in the sample embedding, while true immunological variation sits in the cell code.

2.  Prototype-Driven Cell Typing & Novel Subset Detection  
    • scPoli uses “prototypes” (centroids of known classes) to classify new cells and flag “unknown” ones far from any prototype.  
    • Here you could define prototypes for major immune states (e.g. CD11c⁺ B cells, adaptive NK, CD161⁺ CD4 T) in latent space.  
    • As you profile new cohorts—or time points—you’d automatically classify cells into known states or uncover entirely new rural- or urban-specific subpopulations.

3.  Impute Missing Modalities & Scale to New Assays  
    • A CVAE naturally supports **conditional generation**: given a cell’s latent code plus a modality flag, you can reconstruct any assay’s features (mass-cytometry markers, glycoforms, CITE-seq counts).  
    • That means if only half your donors have CITE-seq, you can still impute protein or transcript levels for the rest—driving deeper integration without throwing away partial profiles.

4.  Reference Mapping Without Retraining  
    • By freezing the CVAE encoder/decoder and merely learning a new sample embedding for each incoming cohort, you’d map new rural/urban populations (e.g. other African or Asian sites) in seconds—no full-model retraining.  
    • That parallels scPoli’s “reference mapping,” letting you continually enlarge the rural–urban atlas.

5.  Generative Counterfactuals & Intervention Modeling  
    • Once trained, you can “dial” a donor’s sample embedding from rural to urban extremes (or tweak its cytokine-sensitivity parameter) and decode what the expected cell-state and glyco-profile would look like.  
    • This would let you simulate metabolic or adjuvant interventions in silico, guiding which pathways (glycolysis vs. FAS vs. PPP) to target experimentally.

6.  Robust Batch Correction & Covariate Decomposition  
    • Instead of MOFA’s global factorization, the CVAE learns to “explain away” known covariates (instrument run, cohort, schistosomiasis status) via conditioning, ensuring residual latents capture only biology.  
    • You can also include continuous covariates (age, lambda trajectory) to sharpen how much each drives variation in each cell type.

By layering the CVAE/prototype paradigm onto this multi-omic, cross-population framework, you’d gain:  
– Clear generative maps between environment → sample embedding → cell states → assay readouts  
– Automatic, scalable reference mapping of new cohorts  
– Out-of-distribution detection of novel immune subsets  
– Imputation of missing assays, reducing cost and increasing power  
– A sandbox for in silico perturbations to guide functional or vaccine studies  

That combination would turn a static multi-omic atlas into a living, predictive model of how urbanization tunes human immunity.

## Causal inference

Here’s how you could layer causal-inference on top of the rural–urban, multi-omic immune atlas—and a survey of the approaches you might reach for:

---

### 1. Frame the Problem Causally  

Before plugging in algorithms, you need to decide what you’d like to call a “cause.”  In this study the *exposures* are things like rural vs. urban environment (plus co-variables like diet, pollutant levels or pathogen burden), and the *outcomes* are shifts in immune cell frequencies, cytokine responses or metabolic enzyme levels.  A causal analysis asks: “If I could intervene on the exposure (move a subject from rural to urban conditions, or reduce their pollutant exposure), what happens to their immune profile?”

---

### 2. Mendelian Randomization (MR)  

•  Uses germline genetic variants as **instrumental variables** for intermediate exposures (e.g. gut‐microbiome composition, metabolic enzyme activity, Fc‐glycosylation traits) that are themselves influenced by environment.  
•  By linking SNP → exposure → immune outcome, MR can give unconfounded estimates of the *effect* of that exposure on immune cell states—even in the presence of unmeasured lifestyle confounders.  
•  Requires large GWAS of the intermediate trait and of the immune phenotype (or QTL for cytokine response).  

---

### 3. Directed Acyclic Graphs & Bayesian Networks  
#### Constraint-based methods (PC, FCI)  
•  Learn conditional-independence relations among *latent factors* (from MOFA) or among *measured features*.  
•  The PC algorithm will orient edges where the data imply “\(A\) d-separates \(B\) from \(C\),” carving out a DAG skeleton and then inferring arrow directions.  

#### Score-based methods (GES, GDS)  
•  Search over DAGs to maximize a penalized likelihood (e.g. BIC) of the multi-omic measurements.  
•  Can be applied to the MOFA latent space (low dimensional) to infer which latent axes “drive” others.

#### LiNGAM  
•  A variant that assumes linear, non-Gaussian relationships and yields fully oriented DAGs.  
•  Could tease out, for example, whether metabolic rewiring in B cells “causes” changes in cytokine output, or vice versa.

---

### 4. Causal-Oriented Search of Multi-Omic Space (COSMOS)  
•  Integrates **prior knowledge** (signaling networks, metabolic pathways, TF–gene regulations) with differential multi-omic readouts.  
•  Estimates TF and kinase “activities” from transcriptome/phosphoproteome, then searches for minimal causal subnetworks linking them to metabolite changes.  
•  Here you could treat mass-cytometry cytokine responses, metabolic enzyme levels and glyco-profiles as “observations” and let COSMOS propose mechanistic paths—e.g. “urbanization → ↑ACC1 in B cells → ↑TNF secretion.”

---

### 5. Essential Regression + Causal Graphical Modeling  
•  ER discovers **latent factors** across all five modalities that predict the rural–urban trajectory λ.  
•  Once you’ve pinned down those key factors, you can run a **Bayesian network** or **structural‐equation model** on just that reduced set, making the causal search tractable even with hundreds of features.  
•  You can then identify which latent factor (e.g. the one loaded on CD11c⁺ B cells + fucosylation) lies “upstream” of TNF production or NK cell adaptation.

---

### 6. Intervention-Style ML: Do-Calculus & Double ML  
•  If you can approximate a “treatment” (urban vs. rural) and some adjustment set of confounders (age, sex, SES), you can apply **targeted maximum likelihood estimation (TMLE)** or **Double/Debiased ML** to estimate the average treatment effect (ATE) of environment on each immune feature.  
•  These methods use modern machine learners to flexibly adjust for high-dimensional confounders without overfitting.

---

### 7. Longitudinal & Mediation Analysis  

•  In an ideal follow-up you’d sample subjects before and after relocation (or controlled dietary/probiotic intervention) and apply **difference-in-differences** or **marginal structural models** to isolate causal shifts.  
•  **Mediation analysis** could then partition how much of the rural→urban effect on cytokine responses is mediated by changes in B cell metabolism vs. NK receptor repertoires.

---

### Key Practical Challenges  

- **Cross-sectional design**: without time‐series or randomization, causal claims rest on untestable no-unmeasured-confounding assumptions.  
- **High dimensionality**: off-the-shelf causal discovery can’t scale to thousands of features—latent-factor pre‐selection (MOFA/ER) or strong priors are essential.  
- **Mixed data types**: integrating continuous (enzyme levels), counts (glyco-peaks), proportions (cell frequencies) and categorical exposures demands flexible likelihoods or residue‐free residualization.  
- **Prior knowledge**: methods like COSMOS or GENESIS shine when you can embed known signaling networks or genotype→expression anchors.  

---

### In Summary  

To move from correlation to causation in this multi-omic atlas, you’d typically  
1. Reduce and denoise (MOFA/ER)  
2. Incorporate genetics or strong priors (MR, COSMOS, GENESIS)  
3. Learn a DAG on latent factors (PC/LiNGAM/GES) or estimate effects via Double ML/TMLE  
4. Validate with perturbations or longitudinal follow-up  

By combining these strategies, you can begin to say not just “these immune features co-vary with urbanization,” but “urbanization causes reprogramming of B cell metabolism, which in turn drives heightened TNF responses.”

## Potential future directions

Building on the rural–urban multi-omic immune atlas, several avenues can deepen our understanding of how environment, metabolism and cell state interact to shape human immunity.  

### 1. Expanding the Multi-omic Landscape

- Integrate **single-cell multi-omics** (e.g., joint scRNA-seq + scATAC-seq, CITE-seq + metabolomics, spatial transcriptomics) to link transcriptional, epigenetic and metabolic programs within individual cells.  
- Add **microbiome profiling** (16S rRNA, metagenomics) to correlate gut and skin microbial consortia with systemic immune phenotypes and trained-immunity signatures.  
- Incorporate **serum and tissue metabolomics/lipidomics** to capture circulating metabolites driving immune cell reprogramming beyond enzyme abundance.  

### 2. Longitudinal and Interventional Studies

- Track **temporal dynamics** of the rural–urban gradient by sampling individuals before, during and after urban transition or controlled environmental interventions (e.g., dietary changes, probiotic administration).  
- Conduct **vaccination trials** within rural and urban cohorts, correlating baseline multi-omic states with antibody titers, B cell glycoforms and memory formation to identify predictors of hyporesponsiveness.  
- Test **metabolic modulators** (e.g., ACC1 inhibitors, glycolysis enhancers) ex vivo and in vivo to directly link metabolic dependencies to functional outcomes and improve vaccine or adjuvant design.  

### 3. Causal Modeling of Environmental Drivers  

- Develop **causal-inference frameworks** that integrate geospatial, pollution and socioeconomic data with multi-omic immune readouts to pinpoint specific exposures (e.g., air quality, pathogen burden) driving immune remodeling.  
- Leverage **Mendelian randomization** or host-genome data to separate genetic predisposition from environmental effects, clarifying gene–environment interactions in rural versus urban immune states.  

### 4. Predictive Computational Models  

- Build **machine-learning models** (e.g., graph neural networks, latent variable models) that fuse high-dimensional omics to predict individual vaccine responses, infection susceptibility or inflammatory disease risk across populations.  
- Implement **transfer-learning pipelines** to map novel cohorts (e.g., other LMIC settings) onto existing atlases, enabling annotation of rare or emerging cell states without full retraining.  
- Create **digital twins** of immune systems by simulating interventions in silico, guiding personalized immunomodulatory strategies based on multi-omic baseline profiles.  

### 5. Linking Adaptive and Innate Immunity 

- Explore how **B cell glycosylation** patterns influence Fc receptor engagement and downstream innate cell activation in rural versus urban settings.  
- Map **T-B cell interactomes** using spatial omics or paired receptor sequencing to understand how metabolic states in one cell type shape partner-cell functionality.  

### Open Research Questions  

1. Which specific microbial taxa or metabolites most potently drive trained-immunity programs in rural populations?  
2. Can baseline metabolic and epigenetic signatures predict who will mount durable memory responses to novel vaccines or infections?  
3. How do changes in antibody glycosylation feed back on immune cell metabolism and signaling circuits?  
4. What are the molecular mechanisms by which urban lifestyles dampen innate signaling sensitivity in NK and monocyte lineages?  
5. To what extent do host genetics versus environment account for interindividual variation in immune-metabolic wiring?  

### Remaining Challenges  

- **Data Heterogeneity & Batch Effects**: Harmonizing assays, platforms and protocols across global sites remains a major obstacle for truly comparable multi-omic analyses.  
- **Cell-type Annotation & Ontologies**: Defining and matching emerging cell subsets across cohorts and technologies demands standardized marker panels and community-curated ontologies.  
- **Scalability & Computation**: Jointly modeling millions of cells with dozens of omic layers requires new scalable algorithms, optimized data structures and federated computing approaches for privacy.  
- **Causal Inference in Observational Cohorts**: Disentangling confounded exposures (e.g., diet, pathogen load, socioeconomic status) to establish mechanistic links calls for robust statistical frameworks and, ideally, controlled experiments.  
- **Temporal and Spatial Resolution**: Capturing the kinetics of immune remodeling and tissue-specific dynamics (e.g., mucosal sites) needs longitudinal sampling and spatially resolved profiling—both logistically and ethically more complex.  

By addressing these directions and challenges, future studies can forge a comprehensive, predictive model of human immunity that spans the molecular to population scales, enabling tailored interventions and equitable health outcomes worldwide.