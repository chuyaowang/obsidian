# Accelerating Clinical Decisions Through Faster Access to Imaging Data

#seminar 

**Speakers:**

* **Elif Sikoglu, PhD:** Senior Medical Director, Perceptive Imaging. Represents the operational and scientific perspective of an Imaging Contract Research Organization (CRO).
* **Daniel J. Rafter, MD:** SVP, Partner & Product Strategy, Flywheel. Represents the technology platform and strategic data management perspective.
* **Yvette Toivola, PhD:** VP, Product Management, Flywheel. Moderator.

---

## 1. Context: The Clinical Trial Imaging Lifecycle and Operational Complexity

**Topic:** The foundational workflow of imaging data within regulated clinical trials.

**Challenges & Current State:**
Elif Sikoglu outlines the rigorous, regulated framework of clinical trials. The primary challenge is managing a complex, multi-stage workflow that involves numerous stakeholders (sites, CROs, sponsors) and disparate systems while maintaining strict regulatory compliance (21 CFR Part 11).

* **Startup Complexity:** Before data collection begins, extensive documentation is required. This includes site-facing manuals and internal process documents outlining read methodologies. Systems must be configured for the specific trial, involving imaging databases, analysis workflows, read platforms, and export applications.
* **Site Onboarding:** Sites must undergo feasibility assessments and training. "Test transfers" or phantom scans are often conducted to ensure scanner compatibility before the "First Patient, First Visit."
* **Data Fragmentation:** A major operational hurdle is the fragmentation of data across these systems. Images flow from sites to a central repository, but data must also flow seamlessly to third-party vendors and eventually back to the sponsor. The "export application" is historically a bespoke, complex tool built specifically to format data for the sponsor at the end of the study.

**Methods & Workflows:**
Sikoglu details the standard operational pipeline:

1. **Image Collection:** Sites acquire images (MRI, PET, SPECT, etc.) based on the protocol.
2. **Upload & Centralization:** Images are uploaded to a central repository.
3. **Quality Control (QC):** Incoming data undergoes immediate checks (technical parameters, anatomy coverage).
4. **Analysis/Reads:** Data is processed according to the specific "Imaging Charter." This ranges from qualitative reads by radiologists to quantitative analysis (e.g., brain atrophy measurement).
5. **Export:** Traditionally, only the derived data (numerical/categorical results) was exported. Now, there is a demand for the source imaging data itself.

**Panelist Perspectives:**

* **Elif Sikoglu (Operational):** Emphasizes that this is not just moving files; it is a "data journey" that requires scientific oversight at every step. She notes a shift from purely categorical endpoints (e.g., RECIST in solid tumors: "Is the tumor bigger or smaller?") to complex **quantitative endpoints** (e.g., brain volume, structural integrity in CNS trials) and **exploratory endpoints** (e.g., Radiomics). This increases the complexity of the data being managed.

---

## 2. The Strategic Problem: The "Data Swamp" and Disconnected Ecosystem

**Topic:** The systemic inefficiencies in how the industry handles the massive volume of imaging data generated.

**Challenges:**
Daniel Rafter argues that while the industry is generating petabytes of high-value data, it is failing to utilize it effectively due to a disconnected ecosystem.

* **The "Black Box" of CROs:** Sponsors fund the trials but often have little visibility into the raw data until months after the trial closes. The "evidence" (images) remains with the CRO, while the sponsor only receives the "answer" (tables).
* **The "Data Swamp" Phenomenon:** Moving data to the cloud is a necessary first step but insufficient. Simply dumping terabytes of files into an S3 bucket creates a "swamp"—unsearchable, uncurated, and effectively useless. Without "activation" (indexing, harmonizing), the data is dead weight.
* **Retrospective Access:** Large pharmaceutical companies have "decades" of data locked in past trials (estimated at 5+ petabytes for some large organizations). Retrieving this retrospectively is a massive, multi-year undertaking because the data was never standardized at the source.

**Methods & Strategic Shift:**
Rafter proposes a shift toward "AI-Ready" infrastructure.

* **Golden Data Lake:** The goal is to transform the swamp into a "Golden Data Lake" where data is harmonized. This requires **domain-specific primary analysis tools**. Just as genomics has specific pipelines, imaging requires specialized tools to handle pixel data and DICOM metadata.
* **Sunk Cost vs. Compounding Asset:** The industry must shift from viewing trial data as a single-use "sunk cost" to viewing it as a "compounding asset." By aggregating data across trials, sponsors can build a "ground truth factory" for training future AI models.

**Panelist Perspectives:**

* **Daniel Rafter (Strategic):** Highlights the urgency. "Early movers" are already building these enterprise imaging platforms. Those who don't will be left with "garbage data" while competitors leverage historical assets to simulate trials and refine inclusion criteria.
* **Elif Sikoglu (Collaborative):** Agrees that the "closed loop" nature of trials is outdated. Sponsors now want the raw data during the study to gain early insights, not just the final report.

---

## 3. The Technical Solution: Automated Curation, Provenance, and "Gears"

**Topic:** The specific technical architecture required to solve the "Swamp" problem and ensure regulatory defensibility.

**Methods - The "Flywheel" Approach:**
The discussion details a specific technical implementation using "Gears"—containerized, version-controlled algorithms that automate the "First Mile" of data curation.

1. **Ingestion & Classification:**
    * *Problem:* Users upload wrong files (e.g., a photo of a cat, an X-ray instead of an MRI).
    * *Solution:* Automated gears read DICOM headers to classify the modality and sequence immediately, rejecting non-compliant data at the door.
2. **De-identification:**
    * *Problem:* Privacy risks (HIPAA/GDPR).
    * *Solution:* Configurable algorithms that not only scrub metadata tags but also detect and redact "burned-in" PHI (Pixel Health Information) often found on Ultrasound or secondary capture images.
3. **Automated Quality Control (QC):**
    * *Problem:* Manual QC is slow and prone to error.
    * *Solution:* Algorithms detect motion artifacts, signal-to-noise ratio issues, or protocol deviations instantly.
4. **Provenance & Audit Trails (21 CFR Part 11):**
    * *Requirement:* Regulatory agencies demand to know *exactly* how a result was derived.
    * *Solution:* The system tracks every interaction. If an AI model is used, the system records: Which model version? Trained on what data? Run by whom? When? This "metadata-rich audit trail" is essential for FDA submissions.

**Panelist Perspectives:**

* **Elif Sikoglu:** Confirms these automated steps mirror the manual work CROs currently do but notes that automating them allows for "interoperability." If the sponsor and CRO use a shared platform, the "outlines" (segmentations) drawn by the CRO are immediately visible and reproducible by the sponsor, eliminating the need for complex export/import cycles.
* **Daniel Rafter:** Emphasizes **reproducibility**. It’s not enough to get the data; you must be able to reproduce the pipeline. Containerization ensures that if you re-run the analysis 5 years later, you use the exact same environment and code, yielding the exact same result.

---

## 4. Future Implications: Secondary Use, AI, and In-Silico Trials

**Topic:** What becomes possible when this infrastructure is in place?

**Results & Opportunities:**

* **Real-Time Trend Analysis:** Instead of waiting for a "database lock," sponsors can see trends in secondary markers. If a drug is showing unexpected toxicity or unexpected efficacy in a sub-group, the trial can be adapted or stopped early (saving millions).
* **Rescue of "Failed" Compounds:** Sikoglu points out that many drugs fail their primary endpoint but might work for a specific biological sub-phenotype. With accessible data, researchers can re-analyze old trials with new hypotheses (e.g., "Did it work in patients with high baseline atrophy?") without running a new study.
* **External Control Arms & Simulation:** Rafter envisions a future where historical data is used to create synthetic control arms, reducing the need to recruit placebo patients. This leads to **In-Silico Trials**, where millions of molecule variations are tested against virtual patient cohorts derived from real-world imaging data.

**Panelist Perspectives:**

* **Elif Sikoglu:** Sees "Exploratory Endpoints" becoming "Primary Endpoints" over time. As AI models validate new biomarkers in the background of current trials, those markers will become the standard for the next generation of trials.
* **Daniel Rafter:** Predicts a future where we "enroll fewer people" because existing data answers many questions. He views this as the key to realizing "Precision Medicine"—moving from population-level averages to patient-specific predictions.

---

## Q&A Session Summary

### Q1: Practical First Steps for Implementation

* **Question:** We have existing (legacy) solutions. What are the first practical steps to modernize, and when do we see ROI?
* **Answer (Rafter):** It must be an **Enterprise Initiative**, not a departmental project.
  * *Step 1:* Conduct an audit of current workflows. Identify "duct-taped" solutions (e.g., thumb drives, FTP sites, manual scripts).
  * *Step 2:* Don't try to build it from scratch ("homegrown efforts often fail"). Partner with specialized vendors.
  * *Step 3:* ROI is "exponential but lagging." You invest upfront to clean the data, but the value compounds as the "Golden Lake" grows, eventually enabling rapid AI development that was previously impossible.
* **Answer (Sikoglu):** Engage your imaging experts/CROs early. Don't treat imaging as a black box; integration requires conversation about data specs.

### Q2: Convincing Leadership

* **Question:** How do I sell this to a skeptical leadership team?
* **Answer (Rafter):** Point out the "Nose Blindness." Organizations get used to inefficiency (e.g., "It's normal to wait 6 months for data"). Challenge this norm. Highlight the security risks of current methods (thumb drives) vs. the security of modern platforms.
* **Answer (Sikoglu):** leverage the **Regulatory Argument**. Regulatory agencies are demanding higher data integrity and provenance. A modern platform is not just a "nice to have" for research; it is a "need to have" for compliance and approval.

---

## Comprehensive Summary

### Motivation & Research Question

The central motivation of the talk is the critical inefficiency in the pharmaceutical industry's handling of medical imaging data. While imaging offers the richest source of patient phenotyping, it is operationally difficult to manage. The "Research Question" explored is: **How can modern, cloud-native platforms bridge the gap between clinical trial execution (CROs) and strategic data utilization (Sponsors) to accelerate drug development?**

### Conclusion

The consensus is that the industry is at a tipping point. The traditional model of "Data Silos" (where data dies at the end of a trial) is unsustainable in the age of AI. The solution is the implementation of **"AI-Ready" Data Ecosystems**—platforms that automate ingestion, curation, and harmonization (using tools like Flywheel). This transforms imaging data from a static "evidence file" into a dynamic, queryable asset.

### Limitations & Challenges

* **Legacy Burden:** The sheer volume of retrospective data (petabytes) is a massive barrier. "cleaning up" the past is expensive and slow.
* **Cultural Inertia:** Organizations are "nose blind" to their own inefficiencies. Shifting to an enterprise-wide data strategy requires a culture change, moving away from "project-based" thinking to "platform-based" thinking.
* **Complexity:** Imaging data is exponentially more complex than tabular data. It requires domain-specific tools, not just generic cloud storage.

### Future Steps

* **Immediate:** Sponsors must audit their current workflows and stop the "bleeding" by implementing standardized pipelines for *prospective* (new) trials immediately.
* **Mid-Term:** Begin the slow process of ingesting and harmonizing high-value retrospective datasets to build the "Golden Lake."
* **Long-Term:** Leverage this harmonized data to train Foundation Models, enable In-Silico trials, and drastically reduce the cost and time of bringing new therapies to market by using synthetic control arms and predictive biomarkers.