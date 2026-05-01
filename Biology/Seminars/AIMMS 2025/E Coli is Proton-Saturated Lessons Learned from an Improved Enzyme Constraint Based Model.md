# E Coli is Proton-Saturated: Lessons Learned from an Improved Enzyme Constraint Based Model

**Speaker:** Claudia de Buck, Wageningen University
**Transcribed Text:** `talk4.txt`
#seminar

---

## 1. Contextual Knowledge

To fully understand the talk, the following concepts are essential:

* **Constraint-Based Modeling (CBM):** A framework for studying metabolic networks. Instead of requiring detailed kinetic information for every enzyme, CBM uses physicochemical constraints (like stoichiometry, thermodynamics, and maximum enzyme capacities) to define a space of possible metabolic states.
* **Flux Balance Analysis (FBA):** The most common CBM technique. It calculates the flow of metabolites (fluxes) through a metabolic network at a steady state, typically by optimizing for a specific biological objective, such as maximizing biomass production (growth) or the production of a specific compound.
* **Genome-Scale Metabolic Model (GEM):** A comprehensive, mathematically structured representation of all known metabolic reactions in an organism. GEMs are the foundation for FBA and other CBM studies. The talk mentions `iML1515`, a well-known GEM for *E. coli*.
* **Enzyme-Constrained Models (ecModels):** An advancement over traditional GEMs. These models incorporate constraints on the total amount of protein (or specific enzymes) the cell can produce. This adds a crucial layer of biological realism, as it forces the model to allocate the limited protein resources among different metabolic functions, linking metabolism directly to the proteome.
* **ATP Maintenance:** The energy (in the form of ATP) that a cell must continuously expend to maintain basic cellular functions, such as maintaining ion gradients, repairing macromolecules, and motility. This is a key parameter in metabolic models.
* **Proton Motive Force (PMF):** An electrochemical gradient of protons across a membrane (e.g., the inner membrane of *E. coli*). It is a form of stored energy used to power various cellular processes, including ATP synthesis, transport, and flagellar rotation.
* **Transhydrogenase:** An enzyme that catalyzes the transfer of reducing equivalents between different cofactors, typically NADH and NADPH. The talk discusses reversing the native transhydrogenase to pump protons and contribute to the PMF.

---

## 2. Logical Flow and Sectional Summaries

The talk is structured to first present a broad industrial challenge, propose a specific bioengineering solution, identify the need for a better predictive model, describe the process of improving that model, and finally, present the key insights gained from the improved model.

### Section 1: The Industrial Motivation

* **Challenge:** In industrial microbiology (microbial cell factories), adding oxygen to bioreactors is expensive. It requires increased stirring and cooling, and it leads to a loss of carbon feedstock as CO2. However, oxygen is often necessary because aerobic respiration generates the large amounts of ATP required for cell maintenance and the production of many valuable compounds.
* **Proposed Solution:** The central goal is to decrease the need for oxygen by engineering the microbe to harvest more ATP from its carbon source under low-oxygen (anoxic) conditions. This would lead to higher product yields and lower production costs.
* **Transition:** This sets up the "larger story" and motivates the need for a specific metabolic engineering strategy.

### Section 2: A Specific Metabolic Engineering Strategy

* **Method:** The speaker introduces a specific strategy to improve ATP yield. The plan is to engineer the enzyme Pyruvate Dehydrogenase (PDH) to change its cofactor specificity from its native NAD+ to NADP+. This shift in the NADH/NADPH balance is hypothesized to reverse the direction of a native transhydrogenase complex (PNTAB).
* **Intended Result:** Instead of its usual function, the reversed transhydrogenase would pump protons out of the cell, contributing to the proton motive force. This would generate energy, reducing the cell's reliance on respiration for ATP.
* **Transition:** To test the feasibility and impact of this complex strategy *before* building it in the lab, a reliable *in silico* (computational) model is required.

### Section 3: Evaluating and Improving the Foundational Model (GEM)

* **Challenge:** The speaker, new to the field, decided to evaluate the quality of existing *E. coli* models before building her project upon them. She found that the most widely used model, `iML1515`, had numerous known issues and mistakes that had been identified and fixed by different research groups in parallel. However, this knowledge was scattered across various publications and not integrated into a single, improved model.
* **Method:** The speaker performed a literature review and systematically integrated these disparate corrections into a single, consolidated version of the `iML1515` model.
* **Result & Next Step:** This effort resulted in an improved base model. To prevent the same problem of scattered knowledge from recurring, the speaker plans to publish this new version in a public Git repository as a "standard gym" (likely a typo for "standard GEM"). This format will allow the community to contribute improvements via branches and pull requests, fostering collaborative, linear model development rather than creating more parallel, disconnected versions.
* **Transition:** With a better foundational GEM, the focus shifts to adapting it for the specific conditions of interest: anoxic growth.

### Section 4: Adapting the Enzyme-Constrained Model (ecModel) for Anoxic Conditions

* **Challenge:** Standard GEMs often fail to accurately predict cellular behavior under different conditions because they don't account for limitations in protein expression. The speaker used an enzyme-constrained version of the model to better reflect physiology. She found that simply switching the model from oxic to anoxic conditions (by setting oxygen uptake to zero) gave poor predictions. The underlying assumption that all other physiological parameters (like protein allocation and ATP maintenance costs) remain constant was flawed.
* **Method:** To improve the model's fit to experimental data for anoxic growth, she re-parameterized the model. This involved adjusting parameters related to the total proteome constraint and the ATP maintenance coefficients.
* **Result:** By optimizing these parameters for the anoxic condition, she achieved a much lower error score, creating a more accurate predictive tool for the specific environment relevant to her engineering strategy.
* **Transition:** This improved, condition-specific ecModel could now be used to explore the cell's energy metabolism in more detail, particularly concerning protons, which are central to the proposed engineering strategy.

### Section 5: Uncovering the "Proton-Saturated" State of *E. coli*

* **Method:** Using the refined anoxic ecModel, the speaker investigated proton production and export during glucose metabolism. She ran a simulation where proton export was made "free" (i.e., having no energy cost) to quantify the metabolic burden of this process.
* **Result:** The model predicted that under anoxic conditions (without acid production), *E. coli* produces a significant number of protons that must be actively exported. The simulation revealed that the energetic cost of this proton export accounts for a staggering **40%** of the total energy budget. This finding demonstrates that the cell is under a high energy burden just to maintain its internal pH, a state the speaker describes as "proton-saturated." This insight strongly supports the potential impact of her proposed engineering strategy, which aims to alleviate this very burden.
* **Deeper Analysis:** The model showed that protons are exported via two main routes: the F1F0-ATPase (which consumes ATP to pump protons) and co-export with acetate. A key modeling assumption was highlighted: formate, another major fermentation product, was assumed to be exported without a proton. This means the protons associated with formate production must be exported via the costly ATPase route. The speaker noted that recent literature suggests formate may be co-transported with protons, but the exact stoichiometry is unknown. This is a critical uncertainty that impacts the model's energy calculations.
* **Conclusion:** The analysis confirmed that if the transhydrogenase reaction (PNTAB) could be reversed, it would save a significant amount of energy by reducing the ATP consumed by the ATPase for proton export.

---

## 3. Q&A Session Summary

* **Question 1:** Does the model account for the fact that not all enzymes encoded in the genome are active under all conditions?
  * **Answer:** No, the model does not explicitly account for this. The gene-protein-reaction (GPR) rules do not include regulation, so the base assumption is that if a gene is present, its enzyme can be active. However, the speaker argues that the model still provides good predictions for the overall conversion of glucose to biomass and fermentation products, suggesting it captures the essential metabolic behavior despite this simplification. She acknowledges it's a point to consider.

* **Question 2:** How many moles of protons are exported per mole of glucose consumed?
  * **Answer:** Under the simulated anoxic conditions, for every 10 mmol of glucose taken up, about 8 mmol of protons are exported. The speaker emphasizes that while the ratio is 8:10, the *impact* of making this export "free" on the predicted biomass growth is very significant, highlighting the high energetic cost.

* **Question 3:** The transcription seems to have captured a question about whether the fixes to `iML1515` were already present in a "medium-sized geosterm model" (likely a typo for "GEM-Ecosystem model" or another *E. coli* model).
  * **Answer:** The speaker confirms that the key fixes she implemented are also in the "coil one" (likely referring to the *E. coli* model from another group) but that her version also includes other corrections, such as to gene-protein relationships, that were not in that other model.

---

## 4. Comprehensive Summary

* **Motivation:** The research is driven by the high cost of aeration in industrial bioprocesses. The goal is to metabolically engineer microbes like *E. coli* to produce ATP more efficiently without oxygen, thereby improving yields and reducing costs.

* **Research Question/Central Argument:** Can we develop a more accurate enzyme-constrained metabolic model for *E. coli* under anoxic conditions to reliably predict the effects of a novel energy-conserving metabolic engineering strategy? The central argument is that existing models are insufficient and that a properly parameterized, condition-specific ecModel is necessary to uncover key physiological constraints.

* **Conclusion:** The talk concludes with three main points:
    1. A new, improved version of the `iML1515` GEM was created by integrating scattered fixes, which will be shared via a version-controlled repository to foster collaborative development.
    2. Enzyme-constrained models require condition-specific parameterization (especially for ATP maintenance and proteome limits) to be predictive when shifting between metabolic states like aerobic and anaerobic growth.
    3. The improved model reveals that *E. coli* growing anoxically on glucose is "proton-saturated," meaning it expends a very large fraction of its energy budget (up to 40%) simply exporting protons to maintain pH balance. This highlights a major, previously underappreciated energetic burden and validates the pursuit of engineering strategies that can help alleviate it.

* **Current Limitations & Alternative Perspectives:**
  * **Model Assumptions:** The model assumes all enzymes are active and does not include regulation, which is a significant simplification of cellular reality.
  * **Parameter Uncertainty:** The stoichiometry of proton-formate symport is unknown. This is a key parameter that could significantly change the model's energy calculations. The current model assumes no co-transport, representing a worst-case scenario for the cell's energy budget.
  * **Model Development:** The speaker's work highlights a systemic issue in the field: the lack of centralized, version-controlled model development, leading to duplicated effort and fragmented knowledge.

* **Potential Next Steps:**
    1. **Publish the Model:** Release the improved `iML1515` model in the proposed Git repository to establish a new standard for community-based model improvement.
    2. **Experimental Validation:** Implement the proposed metabolic engineering strategy (modifying PDH and reversing PNTAB) in *E. coli* to experimentally validate the model's prediction that this will improve energy efficiency.
    3. **Refine Proton Stoichiometry:** Conduct experiments to determine the correct proton-formate transport stoichiometry and update the model accordingly for greater accuracy.
    4. **Expand Model Scope:** Incorporate regulatory mechanisms into the GPR rules to create an even more realistic model.
