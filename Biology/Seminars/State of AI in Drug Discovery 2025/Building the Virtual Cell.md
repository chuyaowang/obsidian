# Building the Virtual Cell

**Panelists:**
* **Theofanis (Theo) Karaletsos, PhD:** Senior Director of Artificial Intelligence, Chan Zuckerberg Initiative (CZI)
* **Hani Goodarzi, PhD:** Core Investigator, Arc Institute; Associate Professor, UCSF
* **Emma Lundberg, PhD:** Associate Professor, Stanford; Professor, KTH Royal Institute of Technology
* **Ron Alfa, MD, PhD:** Co-founder and CEO, NOETIK

---

## Executive Summary

This panel discussion convenes four leaders from academia and industry to dissect the ambitious goal of building a "virtual cell." The consensus is that a virtual cell is not a single, monolithic, reductionist simulation of biochemistry, but rather a suite of predictive, data-driven AI models that operate across multiple biological scales. The panelists advocate for a utilitarian approach, starting with models that are immediately useful to biologists—such as predicting cellular responses to genetic perturbations—and progressively building towards a more comprehensive, multi-scale, and multimodal understanding of cellular and organismal biology. Key themes include the critical need for strategic, fit-for-purpose data generation (especially spatial and proteomic data), the shift from using wet labs for hypothesis search to hypothesis validation, and the necessity of community-wide collaboration through competitions and shared benchmarks to tackle a problem far less defined than previous AI triumphs like protein folding.

---

## Contextual Knowledge

* **Virtual Cell:** A conceptual framework for a computational model that can simulate the behavior of a biological cell. Its goal is to predict how a cell will respond to various stimuli, such as genetic perturbations or drugs, and to understand the underlying mechanisms of cellular function in health and disease.
* **Multimodal & Multi-scale Data:** Biological data comes in many forms (**modalities**) like transcriptomics (RNA), proteomics (protein), genomics (DNA), and imaging. These can be measured at different levels of organization (**scales**), from single molecules to cells, tissues, and whole organisms. Integrating these is a grand challenge.
* **Perturbation:** The act of intentionally disturbing a biological system to observe its response. This is a cornerstone of experimental biology. **Genetic perturbations** (e.g., gene knockdowns using CRISPR) are a common way to infer gene function.
* **Spatial Omics:** A revolutionary class of techniques that measure molecular data (like RNA or protein expression) while preserving the spatial context of the cells within a tissue. This allows researchers to study not just what cells are present, but how they are organized and interact in their native environment.
* **Causal Biology:** The study of cause-and-effect relationships in biological systems (e.g., does protein A *cause* disease B?). This is distinct from correlational analysis and is essential for identifying effective therapeutic targets.
* **CASP (Critical Assessment of protein Structure Prediction):** A community-wide, biennial competition that was instrumental in driving progress in protein structure prediction, culminating in the success of models like AlphaFold. It is often cited as a model for how to organize a scientific community to solve a grand challenge.

---

## Delineation of Panel Discussion by Topic

The discussion was organized around four central themes, with each panelist providing a unique perspective.

### Topic 1: Defining the "Virtual Cell"

The panel collectively rejected a narrow, reductionist definition in favor of a broader, more functional, and multi-faceted vision.

* **Theo Karaletsos (CZI):** Proposed a broad vision of a **multi-scale model** that represents biology from the molecular level up to the organism. He emphasized that "virtual cell" is not a single endpoint but a collection of useful models at different levels of abstraction. He sees the popular definition—a model that predicts transcriptomic response to genetic perturbations—as a valid and tremendously useful *initial target state*, but not the final goal.

* **Hani Goodarzi (Arc Institute):** Added a **utilitarian view**. A virtual cell model has succeeded when a cell biologist can use it *in lieu of* an experimental model for initial hypothesis testing. He argued that focusing on perturbation and transcriptomics is a pragmatic starting point because it directly mirrors the primary lens through which systems biology has operated for the past 20 years.

* **Ron Alfa (NOETIK):** Provided a contrast, stating a virtual cell is **not a "bag of biochemistry" simulation**. At NOETIK, the virtual cell is used as a **probe** to build understanding from the single-cell level up to the patient. The immediate goal is to use simulations to understand patient biology in the context of health and disease, making it directly applicable to therapeutic hypotheses today.

* **Emma Lundberg (Stanford/KTH):** Agreed with Ron, highlighting the promise of these models to understand **emergent properties across scales**. She stressed that biology operates across vast scales—from molecular changes to organism-level phenotypes—and the true power of virtual cell models lies in their potential to interpret these complex, multi-scale connections, which are incredibly difficult to measure experimentally.

### Topic 2: Therapeutic Applications

The panelists described a paradigm shift where in-silico models handle initial discovery, allowing expensive lab work to be focused on validation.

* **Theo Karaletsos:** The primary application is to empower **causal biology**—identifying causal targets and patient cohorts for drug discovery. He envisions a future where the laborious "search for hypotheses" is moved from the wet lab to in-silico experimentation. As he puts it, the wet lab shouldn't be a means of search, but a **means of validation**.

* **Hani Goodarzi:** Framed all disease modeling (including cell lines and mouse models) as an abstraction of the true, unattainable system within a patient. He argued that in-silico models have a key advantage: they can **go beyond the ceiling of experimental models**, which are imperfect recapitulations (e.g., a mouse model of a human disease).

* **Ron Alfa:** Described two concrete applications at NOETIK, which works with static, multimodal data from human tumor pathology specimens:
    1. **Understanding Patient Biology:** They simulate the placement of virtual cells in different tissue contexts to build a rich representation space of patient biology, which is then used to identify therapeutic targets or train classifiers for predicting patient response to therapy.
    2. **Simulating Perturbations:** They use the virtual cell to simulate the effect of perturbations on this static patient data, allowing them to perform *in-silico experiments* on data that cannot be physically manipulated.

### Topic 3: The Data Challenge

This was a central theme, with all panelists agreeing that data strategy is paramount and that we are in a new era where AI needs are driving data generation.

* **Emma Lundberg:** Emphasized that we don't yet know which data modalities will be most valuable. While transcriptomics is currently scalable, she champions the importance of **protein-level measurements** (proteomics), as proteins are the direct executors of cellular function and structure. She highlighted the challenge of modeling the sub-cellular scale (molecule-to-cell) and the need for community synergy to generate well-paired multimodal datasets.

* **Ron Alfa:** Stated that NOETIK started from the premise that the necessary data didn't exist and had to be generated. Their strategy is to create **fit-for-purpose, multimodal, and spatial data** from the outset, using images as a core data type across modalities (H&E, protein, spatial transcriptomics). This ensures that tissue context and cellular interactions are embedded in the model from day one. He noted their strategy is constantly evolving as they learn which data provides the most predictive power.

* **Hani Goodarzi:** Made two critical points:
    1. **A New Era:** For the first time, AI/ML experts are telling biologists what data they need, a major shift in the dynamic.
    2. **The Scale of Data:** Drawing a parallel to NLP, where models showed emergent properties after being trained on ~1 trillion tokens, he suggested biology may need even *more* data because it is less information-dense (more redundant) than human language. This means we must invest in improving data generation technologies themselves.

* **Theo Karaletsos:** From an ML perspective, data strategy must be tied to the goal. He differentiated between data for **general pre-training** (modeling "life as it exists" from large public atlases) and data for **specific applications** (honing in on a biological space with targeted perturbations). He argued that designing the data collection strategy and the potential need for a "curriculum" to teach the models is the true frontier, perhaps even more important than the model architecture itself.

### Topic 4: Fostering Collaboration and Defining Success

The panel discussed how to organize the community to tackle such a complex and ill-defined problem.

* **Hani Goodarzi:** Pointed to **CASP** as the success story for protein folding. To replicate this, the Arc Institute has launched the **Virtual Cell Challenge**, an annual competition where teams apply their models to a high-quality, unseen genetic perturbation dataset. The goal is to create an equal footing for comparison and, just as importantly, to build a vibrant community through platforms like Discord where scientists can interact and collaborate.

* **Emma Lundberg:** Agreed that competitions are great anchor points, but highlighted a key difference: the virtual cell problem is **far less well-defined than protein folding**. A virtual cell is expected to have many capabilities across different scales (predicting transcriptomes, cell-cell interactions, etc.). The next major challenge for the community is to converge on a set of **core capabilities and define how to measure success** broadly across all of them, rather than focusing on single-modality benchmarks.

---

## Comprehensive Final Summary

* **Motivation:** The fundamental motivation is to create predictive, computational models that can grapple with the immense complexity of biology across different scales—from molecules to cells to tissues and organisms. This is a task that is intractable with purely experimental methods and is seen as the next grand challenge for AI in biology.

* **Central Argument:** The panel collectively argues that building a "virtual cell" is a pragmatic, step-wise process, not a single moonshot. The path forward is not through reductionist, first-principles simulation, but through data-driven, machine learning models that learn from massive, multimodal, and strategically generated biological data. The immediate goal is to create models that are demonstrably useful to biologists, thereby creating a virtuous cycle where in-silico experimentation accelerates discovery and guides more targeted wet-lab validation.

* **Conclusion:** The concept of the virtual cell is maturing from a vague idea into a tangible, albeit complex, research program. The field is converging on a strategy that prioritizes: (1) A utilitarian focus on useful, predictive models (like perturbation response). (2) A massive, community-wide effort in strategic, fit-for-purpose data generation, with a focus on spatial and multimodal data. (3) The creation of a collaborative ecosystem, anchored by competitions and shared benchmarks, to drive progress in a coordinated way.

* **Current Limitations:**
  - **Ill-Defined Problem:** Unlike protein folding, the "virtual cell" lacks a single, clear objective function, making it difficult to measure success.
  - **Data Bottleneck:** The scale of data required is immense, and the most informative data modalities and combinations are still under investigation.
  - **Correlational Models:** Current AI models are primarily correlational and do not inherently understand causality, which is a key goal of this endeavor.

* **Alternative Perspectives:** The main alternative discussed and rejected by the panel is the idea of a "bag of biochemistry"—a first-principles, physics-based simulation of all molecular interactions in a cell. The panelists favor a more phenomenological, data-driven machine learning approach that learns predictive rules from observation.

* **Potential Next Steps:**
  * **Establishing Standardized Benchmarks:** The community needs to move beyond single-task competitions to define a suite of benchmarks that assess the core capabilities of a virtual cell across multiple scales and modalities.
  * **Scaling Strategic Data Generation:** A coordinated effort, likely involving public-private partnerships, is needed to generate the massive, multimodal, and spatially-resolved datasets required for pre-training next-generation models.
  * **Integrating Causal Inference:** Developing novel AI architectures and training schemes that can move beyond learning correlations to infer and model causal relationships in biological networks.