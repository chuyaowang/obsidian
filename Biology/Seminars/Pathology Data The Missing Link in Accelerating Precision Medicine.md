# Pathology Data: The Missing Link in Accelerating Precision Medicine

#seminar 

> **Nathan Buchbinder**, Chief Strategy Officer, Proscia
> **Ritida Nanda**, Senior Product Marketing Manager, Proscia

---

## 1. Contextual Knowledge Primer

*To fully understand the technical discussions in this talk, the following concepts are essential:*

* **Whole Slide Imaging (WSI):** The process of scanning conventional glass slides to produce digital "slides" or high-resolution images that can be viewed on a computer screen. These files are massive (often ~1GB each).
* **Histopathology:** The microscopic examination of tissue in order to study the manifestations of disease. It involves staining (commonly H&E - Hematoxylin and Eosin) to visualize cell structures.
* **Multimodal Data Integration:** The combination of different types of data—in this context, specifically combining phenotypic data (pathology images) with genotypic data (molecular/genomic sequencing), clinical data (EHR), and outcome data.
* **Real-World Evidence (RWE):** Clinical evidence regarding the usage and potential benefits or risks of a medical product derived from analysis of Real-World Data (RWD) (data relating to patient health status and/or the delivery of health care routinely collected from a variety of sources).
* **Companion Diagnostics (CDx):** A medical device, often an in vitro device, which provides information that is essential for the safe and effective use of a corresponding drug or biological product (e.g., checking for a specific gene mutation before prescribing a targeted therapy).
* **Biomarker Stratification:** The process of dividing a patient population into distinct groups based on specific biological markers to predict response to therapy.
* **Pre-analytic Variables:** Factors that affect the specimen before it is analyzed (e.g., tissue fixation time, staining protocol, scanner type), which can introduce variability in digital pathology.

---

## 2. Sectional Analysis & Summaries

### Part I: The Paradigm Shift – Pathology as a Data Asset

**Speaker:** Nathan Buchbinder  

**Context & Motivation:**  
Nathan Buchbinder begins by contextualizing the current state of medicine through the lens of the genomics revolution. He references Francis Collins' 2003 prediction that therapeutic medicine would be transformed by 2020. Buchbinder argues that this prediction has largely come true, evidenced by the fact that 38% of FDA-approved drugs in 2023 were precision treatments, and 66% of approvals in 2021 were supported by genomics data. However, he highlights a critical disparity: while genomics has rapidly advanced, pathology—which drives 70% of downstream healthcare decisions and 80% of spending—has remained an analog discipline "trapped on glass." Historically, pathologists have acted as "human pattern recognition devices," relying on visual assessment under a microscope. This analog nature has prevented pathology from serving as a data source for precision medicine in the same way genomics has, creating a "missing link" in the biomedical data ecosystem where phenotypic data is largely inaccessible for large-scale analysis.

**Challenges Resolved:**  
The primary challenge discussed is the operational crisis within diagnostic labs, which inadvertently catalyzed the digitization of the field. Buchbinder notes that the US faces a significant shortage of pathologists, with individual workloads increasing by approximately 44% over the last decade to keep pace with rising biopsy rates and case complexity. Initially, the adoption of digital pathology was driven solely to resolve these logistical hurdles—improving workflow efficiency and quality control. However, this shift has now resolved the secondary, more profound challenge of data accessibility. By moving from the microscope to digital images, the field is overcoming the barrier that kept rich phenotypic data locked away from the drug discovery pipeline, transforming a subjective, manual process into a generator of quantifiable biological insight.

**Methods & Approach:**  
The method for unlocking this value lies in the construction of a "Pathology Data Lake" derived from routine diagnostic workflows. Buchbinder details the immense scale of this data, noting that a single whole slide image is roughly one gigabyte, and typical labs generate thousands of these daily. The approach involves leveraging modern platforms (like Proscia’s Concentric) that capture this data at the "point of diagnosis." Crucially, this data is innately structured for innovation because it is generated in a clinical setting where it is already linked to molecular test results, clinical history, and other diagnostic metadata. To bridge the gap between the labs generating this data (supply) and the life sciences companies needing it (demand), Buchbinder introduces "Aperture," an infrastructure solution designed to surface relevant patient data and cohorts from this global network in real-time, effectively "functionalizing" the data for immediate use in R&D.

**Results & Current State:**  
The result of these shifts is that digital pathology is rapidly becoming mainstream, with near-ubiquitous adoption in regions like Northern Europe and usage by approximately 80% of the top 100 life sciences companies. We are seeing a transition where pathology is no longer just a diagnostic endpoint but a "fuel" for the entire precision medicine lifecycle. The creation of these massive, multimodal datasets—linking pathology images with genomic and clinical data—enables the application of diverse AI models, including new foundation models. Buchbinder asserts that this infrastructure is now allowing scientists to potentially run as many experiments "in silico" (computationally) in one week as they could have in five years using conventional methods, fundamentally accelerating the pace of discovery.

### Part II: Case Studies in Precision Medicine

**Speaker:** Ritida Nanda  

#### Case Study 1: Precision in Biomarker Strategy (Discovery/Strategy)

**Context:**  
A pharmaceutical company was developing BRAF-targeted therapies for advanced melanoma and faced a significant blind spot regarding real-world testing practices. While they had access to claims data and Electronic Health Records (EHR), these sources were superficial; they could confirm if a test was positive or negative, but could not reveal the specific methodologies used or the quality of the testing. This lack of granularity posed a risk to trial design, as the company did not know if they were targeting the correct patient population or if the prevalent testing methods in the wild were sensitive enough to detect the mutations they were targeting.

**Method:**  
The team utilized raw pathology data to gain a granular view of the testing landscape. Unlike standard EHR extracts, the pathology data provided access to the full text of reports and the associated images. This allowed the team to investigate the specific assay modalities—differentiating between Immunohistochemistry (IHC), PCR, and Next-Generation Sequencing (NGS)—and to analyze the specific staging of the patients being tested.

**Technical Insight:**  
The technical value of the pathology data was multifaceted. First, it provided confirmed TNM (Tumor, Node, Metastasis) staging, ensuring the focus remained on stage III and IV patients. Second, it revealed the testing modality, which is clinically critical because less sensitive methods (like certain IHC protocols) can miss mutations in heterogeneous tumors. Third, it distinguished whether testing was performed on primary versus metastatic tissue—a crucial distinction given that the concordance rate between these tissue types is only about 67%. Finally, the data included quality metrics like tumor cellularity and specimen adequacy, allowing the team to separate biological negatives from technical failures due to poor sample quality.

**Result:**  
By leveraging this deep phenotypic and operational data, the pharma company was able to validate that their target trial sites possessed the necessary infrastructure (e.g., NGS capabilities) and that their eligibility criteria were realistic given real-world prevalence and testing habits. This moved their strategy from one based on assumptions and high-level claims data to one based on ground-truth diagnostic evidence.

#### Case Study 2: Clinical Trial Recruitment (Development)

**Context:**  
A sponsor developing therapies for Triple Negative Breast Cancer (TNBC) was struggling with an extremely tight recruitment window. In TNBC, the window for therapeutic intervention typically closes within two to three weeks of diagnosis. Traditional recruitment strategies, which rely on lagging indicators or disparate databases, were too slow; by the time a potential patient was identified, they had often already begun standard-of-care chemotherapy, rendering them ineligible for the trial. This inefficiency contributes to the broader industry statistic that only 7% of eligible cancer patients ever access clinical trials.

**Method:**  
The solution involved using the Aperture platform to surface eligible patients at the exact "moment of diagnosis." Instead of waiting for a claim to be processed or a referral to be manually sent, the system analyzed pathology data in real-time as cases were signed out in the lab. This approach prioritized speed and the completeness of the diagnostic workup to ensure immediate eligibility.

**Technical Insight:**  
Pathology data provided unique advantages over other sources due to its temporal specificity and detailed documentation. It captured the exact timestamp of diagnosis, ensuring patients were flagged while the therapeutic window was still open. It went beyond binary positive/negative flags to provide quantitative biomarker thresholds required for precise trial matching. Furthermore, the reports documented whether the diagnostic workup was complete or if further testing was pending, and whether there was adequate tissue quality to meet protocol requirements. Crucially, it allowed the sponsor to verify that the patient had not yet started any contraindicated therapies.

**Result:**  
This method dramatically improved the recruitment process. The sponsor was able to identify eligible patients before they were lost to standard of care, expanding patient access to potentially life-saving therapies. It also allowed them to dynamically target sites with active recruitment potential (real-time patient flow) and reduced screening failures by pre-qualifying patients based on tissue adequacy and biomarker status before they were even formally screened.

#### Case Study 3: Companion Diagnostic (CDx) Validation (Regulatory)

**Context:**  
A diagnostic company was developing an AI-powered Companion Diagnostic (CDx) to predict EGFR mutations in Non-Small Cell Lung Cancer (NSCLC) directly from tissue images. While the algorithm performed well in controlled, internal settings, the company faced a major regulatory hurdle: proving that the AI would remain accurate when deployed in the "real world." Algorithms are notoriously brittle to "domain shift"—variations in how tissue is prepared, stained, and scanned across different institutions—and regulators require proof of robustness against this variability.

**Method:**  
To address this, the company leveraged a diverse pathology dataset to construct a validation cohort that mirrored the messy reality of clinical practice. They did not just need images; they needed images accompanied by detailed "ground truth" labels derived from validated molecular testing (NGS) to serve as the gold standard for accuracy, along with metadata describing the conditions under which the images were generated.

**Technical Insight:**  
The pathology data proved essential because it documented the "pre-analytic variables" that confuse AI models, such as differences in fixation methods, staining protocols, and scanner types. It also provided quantitative quality metrics assessed at 40x magnification, such as tumor cellularity levels and the presence of artifacts. This allowed the company to stratify their validation testing, ensuring the algorithm was tested against (and could handle) low-cellularity samples, different scanner artifacts, and varied staining intensities.

**Result:**  
The outcome was a successful regulatory submission. The comprehensive validation dataset demonstrated that the algorithm was robust enough for diverse institutional deployment, accelerating the time to market. It also provided commercial confidence that the tool would perform reliably in live clinical workflows, not just in a research lab.

#### Case Study 4: Commercialization & Value Demonstration (Market Access)

**Context:**  
A diagnostic lab offering MET amplification testing for lung cancer faced a challenge common in precision diagnostics: demonstrating value. While they could technically identify MET-amplified patients, they struggled to prove to payers and pharmaceutical partners that this testing translated into tangible clinical benefits. They needed to show that their diagnostic precision led to appropriate therapeutic interventions and better patient outcomes, thereby justifying the cost and utility of the test.

**Method:**  
The lab utilized pathology data to create a "closed-loop" evidence generation system. They moved beyond reporting simple diagnostic results to linking those findings with longitudinal treatment and outcome data. This involved using AI to quantify MET amplification levels precisely and then correlating those distinct levels with patient survival and therapy response rates.

**Technical Insight:**  
A key technical component here was the use of AI-powered quantification to eliminate inter-observer variability. MET scoring can be subjective, but AI provided a standardized, analytical validity to the scoring. By linking these precise scores with treatment sequences and survival data, the lab generated "outcomes-linked pathology data." This proved not just that the patient *had* the marker, but that patients *with* the marker who received the targeted therapy actually lived longer or progressed slower.

**Result:**  
This approach successfully generated the real-world evidence needed to support market access and reimbursement. It created new revenue streams for the lab through pharma partnerships (who value this outcomes data highly) and positioned the lab as a strategic partner in the precision medicine ecosystem, capable of delivering insights that drive better patient care.

### Part III: Synthesis and Future Outlook

**Speakers:** Nathan Buchbinder & Ritida Nanda

**Synthesis of Views:**  
Both speakers converge on the idea that the future of precision medicine is fundamentally "multi-omic." They emphasize that the introduction of pathology data is not meant to compete with or replace genomics, transcriptomics, or proteomics. Rather, it acts as the "missing link" that anchors these molecular datasets in the morphological and spatial reality of the tissue. They invoke Dr. Eric Topol’s perspective that medicine requires combining deep genomic insights with the "rich, messy reality of human phenotypes." The consensus is that while genomics tells you what mutations are present, pathology tells you how the disease is actually manifesting in the tissue structure, and the combination of the two is far more powerful than either alone.

**Future Outlook & Next Steps:**  
Looking forward, the speakers predict a shift toward the use of "foundation models" in pathology AI—generalized models that generate embeddings from images without needing task-specific training labels. This will lower the barrier to entry for analyzing vast pathology archives. The ultimate goal discussed is the routine integration of longitudinal outcomes with diagnostic data. By linking the initial biopsy image to the patient's eventual survival and treatment response, the field aims to move from purely *diagnostic* models (what disease is this?) to truly *predictive* models (how will this specific patient respond to this specific drug?). This transition will enable the "In Silico" scale of experimentation mentioned at the start, fundamentally compressing the timelines and costs of bringing new therapies to patients.

---

## 3. Q&A Session Analysis

Below is a detailed breakdown of the questions asked during the Q&A session and the corresponding answers provided by the speakers.

---

**Question 1:** As pathology becomes more digitized, what do you see as the biggest barrier to truly integrating it into precision medicine? Is this a technology question, a data access question, economics, or just entrenched culture?

**Answer (Ritida Nanda):** Ritida Nanda attributes the biggest barrier primarily to **infrastructure and culture**. While the technology for digital pathology exists and labs are rapidly digitizing, and the economic value is becoming increasingly clear, the fundamental issue is the lack of a standardized "connectivity layer." For decades, pharmaceutical companies and diagnostic labs have operated independently without a common, compliant, and incentivized way for pharma to access real-time diagnostic insights from a lab network. Proscia's Aperture platform aims to provide this crucial infrastructure, and once such connectivity is established, the cultural shift towards integrated precision medicine is expected to follow rapidly due to the undeniable value generated. The significance here is that the bottleneck isn't in the raw technological capability of digital pathology itself, but in the interoperability and business models required to leverage it across the ecosystem.

---

**Question 2:** What types of multimodal data linkages have proven most valuable so far, and which are still underexplored?

**Answer (Ritida Nanda):** Nanda states that the **most immediate value** has come from linking H&E (Hematoxylin and Eosin) and IHC (Immunohistochemistry) pathology images with molecular test results such as NGS (Next-Generation Sequencing), FISH (Fluorescence In Situ Hybridization), and PCR (Polymerase Chain Reaction). This integration enables AI models to predict expensive molecular tests directly from routine stains, streamlining workflows. However, she identifies the linkage of pathology with **longitudinal treatment and outcome data over time** as significantly **underexplored but highly promising**. Most current pathology AI focuses on diagnostic data from a single point in time. Connecting initial biopsies to long-term treatment response, patient survival, and resistance patterns could uncover truly *predictive* biomarkers, not just diagnostic ones, representing the "next generation" of precision medicine. The key to unlocking this potential is the "lab-to-clinic" connectivity that has historically been absent.

---

**Question 3:** How do you advise teams that want to begin leveraging computational pathology but aren't yet fully digitized?

**Answer (Nathan Buchbinder):** Nathan Buchbinder acknowledges that many organizations, even among the top life sciences companies, are not yet fully digitized, but most are continuously investing in digital pathology. His advice for teams in this situation is to **"start small, start focused, and scale up from there."** He suggests two main approaches: Firstly, leverage existing pockets of digital pathology within the organization or identify avenues for rapid, targeted digitization for specific use cases. Secondly, focus on high-impact projects. Instead of attempting a universal digitization of entire archives, identify one specific question or study where computational pathology or AI can provide a material impact (e.g., accelerating a study, identifying a new biomarker, or validating a CDx hypothesis). The critical point is that teams don't need to have all data on hand; they can tap into labs that are already digitized, collect data retrospectively or prospectively in digital formats, or digitize targeted cohorts. This strategy reduces the initial barrier to entry and builds a compelling business case for broader digital infrastructure by demonstrating concrete value.

---

**Question 4:** How would you prioritize which pathology data sets are most useful for a given biopharma initiative?

**Answer (Nathan Buchbinder):** Buchbinder emphasizes that prioritizing pathology datasets should fundamentally align with the principles of good science. The answer should always be dictated by the **unanswered scientific question, the specific hypothesis being tested, or the program's objectives.** Researchers should clearly define their clinical endpoints and the analyses required to make go/no-go decisions for a given compound, target, or trial. He stresses the importance of **not compromising on data quality** based solely on what's immediately available. Instead, teams should proactively seek out the comprehensive, real-world, well-validated, and traceable data needed to successfully execute their studies. This involves putting pressure on data providers to ensure the data is reflective of real-world scenarios and allows for traceability and additional requests, ensuring that the prioritized datasets directly support the scientific inquiry.

---

**Question 5:** Is MET amplification (AI-powered quantification in parentheses) utilized in clinical practice now?

**Contextual Knowledge:** MET (Mesenchymal-Epithelial Transition) amplification is a genetic alteration that can drive certain cancers, particularly non-small cell lung cancer, gastric cancer, and kidney cancer. AI-powered quantification refers to using artificial intelligence to precisely measure the degree of MET amplification from pathology slides, often improving accuracy and consistency compared to manual assessment.

**Answer (Nathan Buchbinder):** Buchbinder confirms that MET amplification is a robustly studied and invested-in area, with its use as a target starting to see some adoption for specific cancers like non-small cell lung cancer, gastric cancer, and kidney cancer. However, he notes that it has **not yet achieved rapid, full-scale clinical adoption** in mainstream practice. He highlights that this question underscores a valuable insight: incorporating pathology data into a multimodal approach provides a better understanding of what tests and methodologies are actually being performed in routine practice. This understanding is crucial for preventing approaches developed in research from facing significant challenges in mainstream diagnostic contexts once a target makes its way to market.

---

**Question 6:** What data is integrated with the Aperture concentric solution? (Specifically asking about omics data, radiomics, pathoomics, and algorithms used.)

**Answer (Ritida Nanda):** Nanda clarifies that the Aperture concentric solution primarily collects **digital pathology images** (whole slide images) through the Concentric platform. This core data is then linked to a rich array of additional information, including **AI-derived biomarkers** (insights extracted from the images by AI), **molecular and genomic results**, and comprehensive **clinical and diagnostic data**. The clinical data encompasses patient records, case information, and the diagnostic context. Furthermore, the platform is tokenized, allowing for seamless linkage to any retrospective and real-time data sources available, thereby creating a "complete patient view" data model.

---

**Question 7:** How does your partnering/collaborating process work for groups with large pathology archives (e.g., H&E, IHC)?

**Answer (Nathan Buchbinder):** Buchbinder explains that Proscia's collaboration process with groups possessing large pathology archives begins by deploying their core digital pathology platform, Concentric. Concentric serves as the operating system for image-based workflows, providing a place for the images and data to be viewed, managed, organized, and analyzed. Once this software is in place, Proscia manages the ingestion of the archive data not only into Concentric but also its linkage into Aperture, which then feeds the real-world data lake for real-time patient surfacing and retrospective cohort assembly. From a functional perspective, Proscia focuses on two avenues: demonstrating the immediate internal value their offerings can create for the partner's data (e.g., fueling research, education, or collaborations), and then, by deeply interrogating that data, identifying opportunities to drive external engagement with biopharma partners who are seeking such data for their R&D efforts.

---

**Question 8:** How generalized is the AI assistance implemented by the Proscia platform from a back-end point of view? Is it a one-size-fits-all solution for different cancer types, or are there several at play?

**Answer (Nathan Buchbinder):** Buchbinder details that the AI within Proscia's platform (Concentric and Aperture) operates in **two main flavors**. The first type comprises **indication-specific AI applications** that are highly specialized for a particular cancer type, tissue type, or indication (e.g., a specific breast panel for HER2, ER, PR, KI-67). Proscia boasts over 120 such applications covering a wide range of therapeutic areas. The second, more generalized type of AI leans into modern concepts like **foundation models and generating embeddings from rich data**. These applications are designed to drive insights that are not tissue- or cancer-type dependent. Instead, they translate images directly into numerical representations that can be leveraged downstream to extract insights without requiring specific pre-training for a narrow dataset. This dual approach allows for both highly targeted analysis and broad, explorative data interrogation, leveraging the best of both specialized and generalized AI.

---

**Question 9:** Does it offer to analyze this per participant patient sample for diagnosis or does it offer biobank scale research?

**Answer (Ritida Nanda):** Nanda confirms that Aperture does indeed offer data at the **individual patient level**. This capability allows users to query patient populations based on a very specific set of inclusion and exclusion criteria. Consequently, it enables precise cohort identification for use cases such as clinical trial recruitment or biomarker prevalence research. This highlights the platform's utility for granular, patient-centric investigations, rather than just aggregate, de-identified biobank-scale analyses.

---

**Question 10:** Does Proscia provide regulatory submission service for FDA approval?

**Answer (Nathan Buchbinder):** Buchbinder clarifies that Proscia **does not directly provide regulatory submission services** (i.e., they don't submit the individual applications for products developed using their software). However, they offer **extensive support** throughout the regulatory process. Their platform itself is FDA 510(k) cleared for use in primary diagnosis, classifying it as a medical device. It also supports regulated studies under GLP (Good Laboratory Practice) and GCP (Good Clinical Practice) guidelines. Proscia provides all necessary documentation for data management, analysis, and AI image analysis results, making the submission process significantly easier for their partners. They also actively triangulate with partners' existing CROs (Contract Research Organizations), such as IQVIA and LabCorp Drug Development, to expedite submissions. This demonstrates Proscia's role as an enabling technology and supportive partner in regulatory processes, rather than a direct submission agent.

## 4. Comprehensive Summary

### Motivation & Central Argument

The central motivation of the presentation is to address the diminishing returns of a purely genomics-focused approach to precision medicine. While genomics has driven the last two decades of progress, the speakers argue that the exclusion of pathology data—the most direct phenotypic representation of disease—has created an efficiency ceiling. The central argument is that pathology must transition from a subjective, analog art form into a quantitative, digital data asset. By doing so, it can provide the "missing link" of context (spatial, morphological, and quality-based) that is necessary to validate molecular findings, recruit patients effectively, and design robust clinical trials.

### Key Findings & Methodology

Proscia proposes a platform-based methodology (via their products Concentric and Aperture) to connect the "supply" of data in diagnostic labs with the "demand" in biopharma. Through four detailed case studies, they demonstrate that:

1. **Context is King:** Molecular results (e.g., BRAF status) are often unreliable without the contextual metadata (cellularity, staging, testing modality) that only pathology provides.
2. **Time is Critical:** In fast-moving diseases like TNBC, the ability to surface patients at the exact moment of diagnosis is the only way to beat the clock on trial eligibility.
3. **Variability is Valuable:** For AI to work in the real world, it must be trained on the "messy" variability of real-world labs, not just curated datasets.

### Conclusion & Future Outlook

The speakers conclude that the industry is rapidly moving toward a "Multi-omic standard," where the integration of pathology images, genomic data, and longitudinal outcomes becomes routine. This convergence is expected to unlock "In Silico" experimentation, allowing researchers to model and simulate trials computationally at a massive scale before moving to physical testing. The ultimate vision is a healthcare system where every patient's diagnostic data contributes to a real-time intelligence engine that accelerates the development of therapies for future patients.

### Limitations & Challenges

Despite the optimism, the talk highlights significant limitations. The primary barrier is not technological but **infrastructural and cultural**. There is no standardized "connectivity layer" to easily move data between independent diagnostic labs and pharmaceutical companies, and these entities have historically operated in silos. Additionally, while digitization is growing, it is not yet universal, meaning many potential data sources remain analog. Finally, the sheer variability of pre-analytic variables (staining, scanning) remains a challenge for the generalizability of AI models, necessitating the use of advanced foundation models.

### Next Steps

The immediate next steps identified involve the broader adoption of **foundation models** to generate insights from unstructured images without the need for labor-intensive annotations. Simultaneously, there is a push to move beyond diagnostic linkages to **longitudinal outcome linkages**, connecting the pixels of a biopsy slide to the survival data of the patient years later. This full-cycle data loop is presented as the next frontier for predictive precision medicine.
