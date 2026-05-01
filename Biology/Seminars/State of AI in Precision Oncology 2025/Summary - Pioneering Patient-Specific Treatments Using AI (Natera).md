# Pioneering Patient-Specific Treatments Using AI

**Summit:** State of AI in Precision Oncology 2025 *(Sponsored Session)*

**Speaker:**
- **Helio Costa, PhD** — Head of Therapeutics, Natera; Adjunct Clinical Assistant Professor, Department of Pathology, Stanford University School of Medicine

**Host:** Kevin Davis (standing in for Doug Flora)

---

> **Relevant Link:** [Digital Twins for Health Society (DT4HS)](https://dt4hs.org/about-dt4hs/) — a society referenced in the summit context exploring digital twin applications in healthcare.

---

## Overview

This sponsored session by Natera presents the company's evolving AI and machine learning capabilities in oncology, centered on its unique position as the operator of one of the world's largest longitudinal, multimodal cancer biospecimen and data repositories. Helio Costa outlines how Natera is moving from diagnostic testing into AI-powered clinical decision support, using foundation models trained on circulating tumor DNA (ctDNA), whole exome/genome sequencing, RNA sequencing, and digital pathology to build what the company calls a "Discovery to Care" AI platform. The session's centerpiece is Natera's **digital twin** concept — a patient-specific in-silico simulation powered by AI agents that can answer clinical questions about treatment response, recurrence risk, and trial eligibility in real time.

---

## Natera's Data Foundation

Natera began in women's health with the development of Panorama, a non-invasive prenatal test, which built foundational capabilities in distinguishing self from non-self DNA in liquid blood draws. The company has since expanded into oncology and organ health (kidney transplant rejection, kidney disease assessment).

The key to Natera's AI ambitions is the data generated through its commercial testing operations. The flagship oncology product, **Signatera**, is a personalized, tumor-informed liquid biopsy and minimal residual disease (MRD) test. Here is how it works:

1. A patient undergoes surgical tumor resection.
2. Natera sequences the tumor tissue (whole exome sequencing) and identifies the patient's specific somatic mutational signature.
3. A bespoke multiplex PCR test is developed to follow that exact mutational fingerprint in the blood over time.
4. Serial blood draws then allow longitudinal monitoring of circulating tumor DNA (ctDNA) levels — for MRD detection, therapy response assessment, and relapse prediction.

Across hundreds of thousands of patients who have received over a million Signatera tests, Natera has accumulated what it claims is the largest corpus of early-stage cancer sequencing and multimodal biomedical data. Crucially, most Signatera patients are **early-stage** (stages I–III), making this dataset uniquely suited to understanding cancer evolution before it reaches advanced, heterogeneous states.

---

## The Signatera Product Suite

Costa walks through Natera's current oncology testing portfolio:

| Product | Description |
|---|---|
| **Signatera** | Tumor-informed personalized MRD/ctDNA test (launched 2019; first MRD assay to market) |
| **Signatera Genome** | Ultra-sensitive version for tumors with very low ctDNA shedding |
| **Latitude** | Tissue-free version of Signatera for patients with unavailable or scarce tumor tissue |
| **Altera** | Comprehensive genomic profiling (CGP) — DNA + RNA sequencing for biomarker-driven therapy selection |
| **Empower** | Hereditary cancer genetic testing |

Signatera has progressively expanded Medicare coverage across colorectal cancer (CRC), pan-cancer immuno-oncology (IO) monitoring, bladder cancer, and more.

---

## ctDNA as a Prognostic and Predictive Biomarker

Costa emphasizes that the quantitative level of ctDNA in blood — measured in mean tumor molecules per milliliter (MTM/mL) — is highly informative:

- **Higher MTM/mL** is associated with higher relapse risk.
- **Lower MTM/mL** generally corresponds to lower relapse risk.
- **Serial measurements** reveal molecular dynamics: rising ctDNA signals molecular disease progression; falling ctDNA signals molecular response.

This longitudinal ctDNA data, combined with whole exome sequencing, RNA sequencing, digital pathology images, and EMR data, creates a rich, multimodal corpus that Natera uses to train foundation models. The resulting models can prognosticate patient outcomes, predict response to specific therapies, and simulate clinical trial scenarios for individuals or patient cohorts.

---

## The Discovery to Care AI Platform

Natera has organized its AI capabilities into a structured platform flowing from left to right:

**1. Data Commons (left)**
All data — whole exome, whole genome, transcriptome, imaging, clinical outcomes, and EMR — is formatted and structured into an AI-ready data lake.

**2. Foundation Model Training (middle)**
Genomic foundation models are trained on DNA, RNA, and imaging data. The ultimate goal is a single unified multimodal foundation model that integrates all data modalities. These models are not directly user-facing; they power downstream applications.

**3. Application Layer (right)**
The applications that clinicians and researchers actually interact with:

- **Digital Twins**: The company's flagship innovation — a patient-specific in-silico simulation system (see below).
- **Clinical Trial Matching**: Match patients to trials based on molecular and clinical data, or reverse-match (identify patients meeting a given trial's criteria).
- **Immunotherapy Response Prediction**: Leverages immunogenomics tools including NeoSelect and NeoPredict.
- **Personalized Cancer Therapy Development**: An end-to-end analytical system for developing patient-specific treatment strategies.

---

## Immunotherapy: NeoSelect and NeoPredict

Tumor neoantigens — mutated peptide sequences displayed on the surface of cancer cells — are key determinants of whether the immune system can recognize and attack a tumor. Natera has developed **NeoSelect**, a neoantigen prediction tool, which Costa reports outperforms all 25 competing state-of-the-art tools in a benchmarking study (highest percentage of correct neoantigen predictions against a gold standard).

Building on this, **NeoPredict** uses neoantigen prediction to forecast patient response to immunotherapy. Costa shows that NeoPredict achieves greater separation between responders and non-responders than the current standard of care metric — tumor mutational burden (TMB).

---

## Digital Twins: The Core Innovation

The digital twin concept is the conceptual center of the session. The idea is to use all available multimodal patient data to create a virtual patient that can be queried in natural language to answer specific clinical questions.

**Architecture:**
- Inputs: tumor and germline DNA, RNA, serial ctDNA from Signatera, digitized H&E slides, clinical outcomes, and EMR data.
- These inputs feed into specialized AI agents — purpose-built for genomics, histology, literature review, EHR interpretation, and dozens of other domains.
- When a clinical question is posed, the digital twin coordinates the relevant agents in real time and synthesizes their outputs into a single holistic recommendation.

**Clinical Use Case Examples:**

*Use Case 1 — Treatment Selection:*
"Which treatment works best for patients most similar to mine, and why?"
A stage III breast cancer patient undergoing neoadjuvant chemotherapy. The system pulls Signatera post-op baseline, clinical data, H&E slides, Altera CGP profiling, and tumor microenvironment data. Output: predicted likelihood of treatment response with grounding in data and literature references, similar historical patient trajectories, alternative regimen options, and matched clinical trials.

*Use Case 2 — Recurrence Risk and Adjuvant Therapy:*
"What is my patient's risk of recurrence, and should I escalate to adjuvant therapy?"
A stage IIB breast cancer patient. Output: quantified recurrence risk, adjuvant therapy recommendation, ctDNA-based surveillance schedule, follow-up imaging suggestions, and clinical trial options.

*Use Case 3 — Clinical Trial Eligibility:*
"Is my patient eligible for an ongoing clinical trial?"
A lung cancer patient with defined mutations. Output: recurrence likelihood stratified into risk buckets, rank-ordered treatment options with predicted response probabilities, top matched clinical trials, and tiered guideline-based care recommendations.

---

## Beyond Individual Patients: Population-Level Modeling

In addition to single-patient queries, Natera is building browser-based tools for visualizing individual disease trajectories graphically — allowing clinicians to toggle through different intervention scenarios and see how they change predicted outcomes. The same tools can be applied to patient cohorts: all patients in a clinic, all patients of a given subtype, or all patients who received a specific therapy, enabling population-level trend analysis to inform practice-wide management decisions.

---

## Strategic Positioning and Future Direction

Costa concludes by framing Natera's commercial diagnostic operation — generating longitudinal, multimodal real-world data across hundreds of thousands of patients — as a durable competitive moat for AI development. The combination of proprietary data from commercial testing, clinical trial partnerships, and access to structured and unstructured EMR data creates what he calls "a robust basis for a new paradigm of AI-enabled healthcare." The company's stated end-use goal is to accelerate patient management and care, clinical development, and biomedical research and discovery.

---

## Key Takeaways

**Longitudinal ctDNA data is uniquely powerful for AI training.** Most AI in oncology is trained on snapshots; Natera's serial Signatera data creates true longitudinal trajectories that enable dynamic, time-aware predictive models.

**Early-stage patient data is the most strategically valuable.** Because most Signatera users are early-stage patients, Natera has deep data on the early phases of cancer evolution — the period when interventions are most likely to be curative and when predictive models can have the greatest impact.

**The digital twin is an orchestration layer, not a single model.** Its power comes from coordinating many specialized agents — each an expert in one data type or domain — into a coherent clinical recommendation. This architecture scales as new data modalities and new agents are added.

**The session is a product demonstration as much as a scientific talk.** While the clinical use cases are compelling, most of the evidence presented is benchmarking or illustrative rather than prospectively validated clinical outcomes data. The digital twin platform appears to be in an active development and early deployment phase.
