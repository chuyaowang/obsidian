# Weighted metrics are required when evaluating the performance of prediction models in nested case–control studies

#paper 
[link](https://bmcmedresmethodol.biomedcentral.com/articles/10.1186/s12874-024-02213-6)


## 1. Motivation

The authors are motivated by the practical challenge of validating risk prediction models when using nested case–control (NCC) study designs. In many clinical research settings—especially when outcomes are rare or predictors are costly or hard to obtain—it is inefficient or even infeasible to measure everything in a full-cohort study. NCC designs enable researchers to focus on a subsample (including all cases and a fraction of the controls), but this sampling introduces bias in standard performance metrics (e.g., _discrimination_ and _calibration_ measures). The authors, therefore, aim to develop and recommend weighted performance metrics that adjust for the overrepresentation of cases and the non-representative control sampling in NCC studies.


> [!info]- NCC and discrimination and calibration measures
> ### 1. What Is the NCC Study Design?
> 
> **Nested Case–Control (NCC) Design** is a type of two-phase sampling design used within a well-defined cohort. In an NCC study, researchers first follow a large cohort over time and then—once events (cases) occur—they select all (or a sample of) those cases and a sample of controls from the remaining members of the cohort. The controls are chosen from the subjects who are still "at risk" of the event at the time each case occurs (often through a method called incidence density sampling).
> 
> Key points include:
> 
> - **Case Inclusion:** All subjects who develop the outcome (or a pre-specified sample of cases) are included.
> - **Control Sampling:** Controls are randomly drawn from those who have not yet experienced the event at the time of each case’s occurrence. This selection maintains the temporal aspect of risk.
> - **Matching (Optional):** Often, the design involves matching controls to cases on variables like age, sex, or follow-up time to control for confounding.
> - **Weighting:** Because the control group is a sub-sample and its risk factor distribution may be distorted (e.g., longer surviving individuals might be overrepresented), each subject is assigned a weight—the inverse of their sampling probability—to reconstruct the distribution in the full cohort. 
> 
> This design is especially efficient when the outcome is rare or when certain predictors are expensive or challenging to collect, allowing validity without the cost of full-cohort data collection.
> 
> ---
> 
> ### 2. What Are Calibration and Discrimination Measures?
> 
> These are two core types of performance metrics used for evaluating risk prediction models.
> 
> #### **Discrimination Measures:**
> 
> - **Definition:** Discrimination refers to how well a prediction model distinguishes between individuals who will experience the event of interest and those who will not.
> - **Example Metric:** The **C-index** (or area under the receiver operating characteristic curve, AUC) is commonly used. It represents the probability that, for a randomly chosen pair of individuals (one with and one without the event), the one with the event has a higher predicted risk.
> - **Use:** In clinical prediction, discrimination tells you if the model can correctly rank subjects by their risk. A higher C-index indicates a better ability to separate high-risk from low-risk individuals.
> 
> #### **Calibration Measures:**
> 
> - **Definition:** Calibration evaluates the agreement between the risk predicted by the model and the actually observed outcomes.
> - **Key Indicators:**
>   - **Calibration Slope:** This is derived from a regression of the observed outcomes on the model’s predicted risk. A slope of 1 indicates perfect calibration; slopes below 1 suggest that the predictions are too extreme (overfitting), while slopes above 1 indicate underfitting.
>   - **Observed-to-Expected (O/E) Ratio:** This compares the actual number of events (observed) with the number of events predicted by the model. An O/E ratio close to 1 implies that the model is well calibrated; significant deviations point to systematic over- or underestimation of risk.
> - **Use:** Calibration judges whether the absolute risk estimates are accurate. For instance, if a model predicts a 20% risk for a group, calibration should verify that about 20% of that group indeed experiences the event.
> 
> ---
> 
> ### 3. What Are They Used For?
> 
> Both discrimination and calibration metrics are used to gauge different aspects of a predictive model’s performance:
> 
> - **Discrimination** is used to assess how well a model differentiates between those who will and will not experience the event. It is critical for ranking patients (or subjects) by risk and is especially important when making decisions about who might require more intensive intervention.
> 
> - **Calibration** is used to assess whether the predicted risks match the actual risk levels. This is crucial for decision-making in clinical settings where predicted probabilities (absolute risk estimates) inform treatment or screening decisions. For example, if a model is used to determine eligibility for preventive therapy, having well-calibrated risk estimates ensures that patients aren’t overtreated or undertreated.
> 
> In NCC studies, the performance metrics (both discrimination and calibration) need to be adjusted by weighting the subjects appropriately. This compensation mitigates the biases introduced by the NCC sampling (e.g., overrepresentation of cases or altered control risk factor distributions) so that the estimated performance metrics reflect what would have been observed had the full cohort been used.
> 
> ---
> 
> ### Summary
> 
> - **NCC Study Design:** Involves sampling all cases from a cohort along with a sub-sample of controls from those at risk at the time of each case; it is efficient for rare outcomes and expensive predictors and requires weighting to adjust for sampling biases.
> - **Discrimination Measures** (like the C-index) assess how well the model separates high-risk from low-risk subjects.
> - **Calibration Measures** (like the calibration slope and O/E ratio) assess whether the model’s predicted probabilities correspond to the observed event rates.
> - **Usage:** Both types of measures are key for validating clinical prediction models—discrimination for ranking risk and calibration for verifying that the risk estimates are accurate.
> 
> Together, these concepts ensure that risk prediction models are both accurate in ranking patient risk and reliable in their absolute risk predictions, which is critical for making informed clinical decisions in settings such as screening, preventive care, or targeted treatment interventions.


---

## 2. Research Question

The paper asks: 

**How can the performance of prediction models (in particular, discrimination and calibration measures) be correctly evaluated in nested case–control studies?**

It tackles the challenge of recovering unbiased estimates of performance metrics—even in scenarios where the controls’ risk factor distributions have been distorted by the NCC sampling procedure—by proposing a weighting framework based on each subject’s inverse sampling probability.

---

## 3. Relevant Background Information

Several strands of background information set the stage for this work:

- **Risk Prediction Models in Epidemiology:**  
  Large population-based cohorts are ideal for developing and validating risk prediction models. However, when the predictors (such as expensive biomarkers) are costly or hard to measure, and when the target outcomes occur infrequently, studying the entire cohort may be impractical.

- **Nested Case–Control Study Design:**  
  In NCC studies, all cases (subjects who develop the outcome) are included along with a random sample of controls (subjects who do not develop the outcome) from the full cohort. Often, additional matching (e.g., on sex or age) is performed to reduce confounding. However, NCC designs inherently alter the proportion of cases and controls relative to the full cohort and may bias the distribution of risk factors.

- **The Need for Adjustment:**  
  Although methods for developing prediction models in NCC data have been explored, there has been less guidance on the proper validation of these models. Without adjustments, performance metrics estimated from NCC data (like the C-index, calibration slope, and decision curve net benefit) can be significantly biased compared to the full cohort.

This background underscores the importance of developing robust statistical adjustments to allow NCC studies to inform clinical prediction accurately without needing to analyze unwieldy full-cohort data.

---

## 4. Relevant Theories

The paper draws upon several theoretical concepts:

- **Sampling Theory and Inverse Probability Weighting:**  
  The concept is that when subjects are sampled with known probabilities, one can “undo” the bias by weighting each subject by the inverse of their probability of selection. This allows the NCC data to be “reconstructed” to mirror the full cohort in terms of case-to-control ratio and variable distribution.

- **Performance Metrics for Risk Prediction Models:**  
  - **Discrimination (C-index):** Measures the model’s ability to correctly rank subjects by risk.  
  - **Calibration (Calibration Slope, Observed-to-Expected Ratio):** Assesses how closely the model’s predicted probabilities match the observed event rates.  
  - **Decision Curve Analysis:** Evaluates the clinical utility of a model by weighing the benefits of true positives against the harms of false positives across various threshold probabilities.

- **Matching and Incidence Density Sampling:**  
  These are well-established methods to select controls in NCC designs so that—in theory—the controls represent the pool of subjects at risk at each case’s event time.

By integrating these theories, the authors argue that proper weighting (using inverse probability weights computed by methods such as Kaplan–Meier estimates, logistic regression, or generalized additive models) can remove the bias introduced by the NCC design.

---

## 5. Methods

The study proposes a detailed framework for adjusting performance metrics in NCC datasets:

- **Weight Calculation:**  
  Each subject’s weight is defined as the inverse of their probability of being sampled. Cases usually have a sampling probability of 1 (or a fixed value if only a subset is sampled), whereas controls have weights that may vary and tend to be higher when their sampling probability is lower. The paper describes methods (using Kaplan–Meier, generalized linear models, or generalized additive models) to compute these probabilities and then rescale the weights so that the sum approximates the original cohort size.

- **Weighted Performance Metrics:**  
  The authors modify standard metrics:
  - **C-index:** They extend the concordance calculation by weighting each pair of subjects by their respective weights.
  - **Threshold-Based Metrics:** Sensitivity, specificity, PPV, and NPV are recalculated using the weights to account for the altered case–control ratio.
  - **Calibration Measures:** The observed event rates (or survival probabilities) and predicted risks are aggregated with weights, resulting in unbiased estimates of the calibration slope and observed-to-expected ratios.
  - **Decision Curve Analysis:** The net benefit is computed using the weighted counts of true and false positives.

- **Real-World Illustration:**  
  As a demonstration, the BOADICEA breast cancer risk prediction model was validated using data from the population-based Rotterdam Study. The authors compared metrics computed on the full cohort with those on several NCC datasets (derived via both unmatched and matched designs, and using different control-to-case ratios) and evaluated the performance before and after weight adjustments.

---

## 6. Results

Key findings include:

- **Bias in Unweighted Metrics:**  
  The paper reports that performance measures (e.g., the C-index and the observed-to-expected ratio) computed in NCC datasets without adjustment are significantly biased. For example, unweighted C-index values were notably lower than those from the full cohort.

- **Improvement with Weighting:**  
  When applying the proposed inverse probability weights, the weighted performance metrics closely matched the values obtained from the full cohort. This was demonstrated across several metrics (discrimination, calibration, and decision analysis) and in both unmatched and matched NCC designs.

- **Robustness of Adjustment Methods:**  
  The authors performed sensitivity analyses using different methods for weight calculation (Kaplan–Meier, GLM, GAM) and varied the number of controls per case. In all cases, the weighting adjustments yielded performance metrics that were consistent with full-cohort estimates.

---

## 7. Validations

The authors undertook extensive validation steps:

- **Repeated Sampling:**  
  They repeatedly derived NCC datasets from the full cohort (100 replications) to account for sampling variability and demonstrated that the weighted metrics remained stable across these replications.

- **Comparative Analysis:**  
  They compared unweighted and weighted metrics directly against the “true” performance as computed from the full cohort. The convergence of the weighted estimates to the full-cohort values confirmed that the adjustments were effective.

- **Use of Multiple Weighting Schemes:**  
  By testing several statistical approaches for estimating sampling probabilities, the authors showed that the general conclusions held regardless of the exact method used to compute weights.

---

## 8. Implications

The innovations in this paper have far-reaching implications:

- **Efficient Model Validation:**  
  The proposed methodology allows researchers to use NCC datasets—which are more efficient and less costly than full cohorts—for accurate validation of prediction models. This is particularly important when assessing models built with expensive, hard-to-obtain biomarkers or when outcomes are rare.

- **Broader Application:**  
  With unbiased performance estimates, NCC designs can be reliably used in both the development and external validation of risk prediction models. The approach is generalizable to various contexts, including survival outcomes and binary outcomes.

- **Methodological Best Practices:**  
  The paper underscores the need for weighted performance evaluation in stratified or oversampled data. It provides a clear guide for how to implement these adjustments, which can improve the quality and reliability of risk prediction research.

---

## 9. Clinical Problem Addressed

In a clinical context, many risk prediction models are used to identify individuals at high risk for diseases (for example, predicting breast cancer risk with the BOADICEA model). However, gathering full-cohort data on expensive biomarkers or long-term outcomes is often impractical. This innovation:
  
- **Optimizes Resource Use:**  
  It facilitates model validation in scenarios where data collection from the entire cohort is prohibitively expensive or logistically challenging.
  
- **Enhances Risk Stratification:**  
  By enabling unbiased estimation of model performance, clinicians can trust that the risk predictions (e.g., for breast cancer) are accurate. This helps guide clinical decisions, such as whom to screen more intensively or which patients might benefit from preventive interventions.
  
- **Improves Personalized Medicine:**  
  Ultimately, the improved validation of risk prediction models via NCC designs can lead to better individualized risk assessments, allowing for more targeted intervention strategies and potentially better patient outcomes in areas such as cancer prevention and early detection.

---

## In Summary

The paper addresses a critical methodological challenge by establishing that the performance of prediction models in nested case–control studies must be evaluated with weighting adjustments to counteract sampling biases. Motivated by the need to validate models efficiently in resource-limited settings, the authors provide both a theoretical foundation in inverse probability weighting and practical weighted formulations for key performance metrics. Through real-world validation using the BOADICEA breast cancer model in the Rotterdam Study, they demonstrate that the weighted metrics recover unbiased estimates comparable to full-cohort measures. The implications are significant, as this approach enables accurate risk prediction and informs personalized clinical decision-making—addressing the broader clinical problem of how to implement and validate high-quality risk models when data from full cohorts are not available.