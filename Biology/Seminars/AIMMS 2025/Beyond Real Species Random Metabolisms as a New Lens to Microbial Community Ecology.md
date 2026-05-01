# Beyond Real Species: Random Metabolisms as a New Lens to Microbial Community Ecology

**Speaker:** Djordje Bajic, Technische Universiteit Delft (TU Delft)
**Event:** Amsterdam Institute of Molecular and Life Sciences (AIMMS) Symposium
**Transcribed Text:** `talk3.txt`
[Review: Structuring complexity by mapping the possible in microbial ecosystems](https://www.sciencedirect.com/science/article/pii/S1369527425000803)
#seminar

---

## Contextual Knowledge (Key Concepts)

* **Optimality vs. Typicality:** A central theme of the talk. The **optimality paradigm** assumes evolution produces organisms that are "the best" at a certain task (e.g., fastest growth). The **typicality paradigm** abandons this, instead assuming that any *viable* solution is possible, and seeks to understand the properties of a *typical* member of that vast solution space.
* **Consumer-Resource Model:** A class of ecological models where species compete by consuming shared resources. The interactions are not direct but are mediated through the depletion and production of resources. The speaker's model is a highly detailed, mechanistic version of this.
* **Genome Streamlining:** An evolutionary process, common in microbes (especially symbionts and pathogens), where genes that are not essential for survival in a particular environment are lost over time, resulting in a smaller, more compact genome. The random deletion of reactions in the model is a simulation of this process.
* **Competitive Exclusion Principle:** A proposition in ecology stating that two species competing for the same limiting resource cannot coexist at constant population values; when one species has even the slightest advantage over another, the one with the advantage will dominate in the long run.
* **Lotka-Volterra Model:** A classic ecological model that describes the dynamics of biological systems in which two species interact, originally predator-prey. It can be generalized to model competition by using a matrix of random interaction coefficients, which is what the questioner in the Q&A was referring to.

---

## 1. Overview and Logical Flow of the Talk

This talk presents a provocative and highly theoretical approach to microbial ecology. The speaker, Djordje Bajic, argues for moving "beyond real species" to understand the fundamental principles governing microbial communities. He proposes using randomly generated, but viable, metabolic networks as a tool to bridge the gap between abstract ecological theory and messy biological data. The central thesis is that by studying the *typical* properties of these random metabolisms, we can uncover emergent ecological patterns that are difficult to explain using traditional models.

The logical flow of the presentation is as follows:

1. **Introduction & A Provocative Question:** The talk opens by contrasting data-heavy biology with abstract theory and poses a thought experiment: If you isolate members of a stable, diverse microbial community, will they coexist in pairs? This question reveals the weakness of our predictive ecological theories.
2. **The Modeling Gap:** The speaker argues that traditional ecological models (e.g., predator-prey) are disconnected from genomic data, while traditional metabolic models are often trapped in an "optimality paradigm" that fails to capture the suboptimal nature of real microbes.
3. **The "Typicality" Paradigm:** The proposed solution is to shift from seeking *optimal* metabolic solutions to exploring the entire space of *possible* (viable) solutions. This is the "typicality" paradigm.
4. **Methodology - Generating "Random Species":** The method for this exploration is introduced. It involves starting with a "universal metabolism" (a network of all known reactions) and then randomly deleting reactions until a minimal, but viable, network is achieved. This process, simulating genome streamlining, generates thousands of unique, suboptimal "random species."
5. **Results Part 1: Realistic Suboptimality:** These random models, despite not being optimized, are shown to have realistic "leaky" secretion profiles. They excrete a variety of metabolites, similar to real organisms, with aerobic models producing CO2 and anaerobic ones producing fermentation byproducts.
6. **Results Part 2: Community Assembly and the Importance of Interactions:** The random species are used to simulate community assembly. These simulations demonstrate that metabolic interactions (cross-feeding) are essential for maintaining species diversity, particularly for sustaining a "rare biosphere" of secondary consumers.
7. **Results Part 3: Solving the Initial Puzzle:** The talk returns to the initial question about pairwise coexistence. The speaker presents experimental data showing that species from a stable community often *fail* to coexist in pairs (they competitively exclude each other). Remarkably, the community models built from the random metabolisms reproduce this exact counter-intuitive pattern.
8. **Conclusion & Q&A:** The talk concludes by reiterating the power of using random metabolisms to bridge theory and data. The Q&A session delves deeper into the choice of substrate, the specific byproducts, and the critical difference between this approach and simpler random interaction models like Lotka-Volterra.

***Note on Transcription:*** *The provided text was machine-transcribed and contained several errors. These have been interpreted and corrected for clarity in this summary. For example, "talk cookers" has been corrected to **talk glucose**, "forment" to **formate**, "emergent per distance" to **emergent pairwise coexistence**, and "lot of altera" to **Lotka-Volterra**.*

---

## 2. Sectional Summaries

### 2.1 Introduction: A Puzzle in Community Ecology

* **Challenge Resolved:** To frame the central problem of the talk. The speaker highlights a disconnect between our ability to observe complex communities and our ability to predict their behavior from first principles.
* **Methods Used:** A thought experiment is posed: Take a stable, multi-species microbial community grown on a single carbon source. If you isolate members and try to grow them together in pairs, will they coexist? The audience's mixed and uncertain response illustrates that our intuition and existing theories are insufficient to answer this.
* **Results:** The ambiguity of the answer serves as the motivation for the entire talk. It suggests we need better models that can connect the properties of individual species to the collective behavior of the community.
* **Leads to Next Section:** This puzzle directly leads to a critique of existing modeling paradigms and the proposal for a new one.

### 2.2 The Gap Between Ecological Theory and Metabolic Data

* **Challenge Resolved:** To identify the specific shortcomings of current modeling approaches in microbial ecology.
* **Methods Used:** The speaker critiques two dominant paradigms:
    1. **Abstract Ecological Models** (e.g., Consumer-Resource, Predator-Prey): These are powerful for generating general theoretical insights but are disconnected from measurable biological data like genomes and metabolic pathways. They can't predict *which* species will be present.
    2. **Genome-Scale Metabolic Models (GEMs):** These are data-driven (built from genomes) but traditionally rely on an **optimality assumption** (e.g., maximizing growth). This leads to the "paradox of optimality": if organisms are optimal, why do they always evolve to be better when put in a lab environment? Real organisms are clearly not optimal.
* **Results:** A gap is identified: we need models that are mechanistically detailed like GEMs but do not rely on unrealistic optimality assumptions.
* **Leads to Next Section:** This sets up the introduction of the "typicality" paradigm as the solution to escape the paradox of optimality.

### 2.3 The "Typicality" Paradigm: From Optimal to Possible

* **Challenge Resolved:** To propose a new conceptual framework for using metabolic models.
* **Methods Used:** The speaker advocates for a shift from an **optimality paradigm** to a **typicality paradigm**. Instead of asking "What is the single best phenotype?", the question becomes "What does a *typical* viable phenotype look like within the vast space of possibilities?" This involves exploring the entire solution space of viable metabolic states, not just a single optimal point.
* **Results:** This conceptual shift allows for the modeling of suboptimal, "leaky" organisms that are more representative of real biology.
* **Leads to Next Section:** The next step is to develop a concrete method for generating a population of these "typical" organisms to study.

### 2.4 Methodology: Generating Random Viable Metabolisms

* **Challenge Resolved:** To create a computational pipeline for generating a diverse set of suboptimal, yet realistic, model organisms.
* **Methods Used:** The process, simulating **genome streamlining**, is as follows:
    1. Start with a **universal metabolic model** containing thousands of known reactions.
    2. Randomly delete reactions from this network.
    3. Continue deleting until a **minimal network** is reached that is still **viable** (i.e., can produce biomass) in a specified environment (e.g., on glucose).
    4. Repeat this process thousands of times to generate a large ensemble of "random species" with different metabolic capabilities (specialists vs. generalists).
* **Results:** This method produces a collection of *in silico* organisms whose genomes have a realistic structure: a core of essential reactions, an accessory set of common reactions, and a large tail of unique reactions.
* **Leads to Next Section:** Now that these random organisms exist, their properties can be analyzed, starting with their metabolic secretions.

### 2.5 Results: Realistic Secretions and Community Assembly

* **Challenge Resolved:** To demonstrate that these randomly generated models exhibit realistic ecological properties.
* **Methods Used:** The metabolic secretions of the random models were simulated. Then, thousands of these models were inoculated into a simulated **community assembly** experiment (akin to a serial dilution).
* **Results:**
    1. **Secretions:** The models were "leaky," secreting a wide range of metabolites. The byproducts made sense chemically: CO2 in aerobic conditions, and methane, formate, and hydrogen in anaerobic conditions. This mirrors the suboptimality of real microbes.
    2. **Community Dynamics:** The assembly simulations showed that metabolic interactions were crucial for coexistence. A control simulation with interactions turned off showed a much faster collapse in diversity. Furthermore, the analysis revealed a clear ecological structure: high-abundance "primary consumers" fed on the main resource (glucose), while a diverse set of "rare" taxa survived by cross-feeding on the secretions of others.
* **Leads to Next Section:** These results show the models can capture complex community dynamics. This prompts a return to the original, more specific puzzle about pairwise coexistence.

### 2.6 Solving the Puzzle: Emergent Pairwise Competition

* **Challenge Resolved:** To test if the random metabolism framework can explain the counter-intuitive experimental observation about pairwise coexistence.
* **Methods Used:** The speaker first presents experimental results from his postdoctoral work, which showed that when isolates from a stable community were co-cultured in pairs, the most common outcome was **competitive exclusion** (one species outcompetes the other), not stable coexistence. He then performed the same pairwise analysis on the members of his simulated stable communities.
* **Results:** The *in silico* experiment with random metabolic models **qualitatively reproduced the experimental finding**. The dominant outcome of pairwise simulations was competitive exclusion, with stable coexistence being rare. This demonstrates that the model, built on the principle of "typical" metabolisms, captures an emergent property of real microbial communities that simpler models might miss. The speaker notes he is still working to understand the precise mechanism behind this.
* **Leads to Next Section:** This is the final result, leading into the conclusion and Q&A.

---

## 3. Summary of the Q&A Session

**Question 1:** Why do the simulations focus so much on glucose? What about other carbon sources?

* **Answer:** They are performing simulations with other carbon sources. However, the system is so complex that they don't yet have a full understanding of the dynamics even on a simple substrate like glucose. The focus is on understanding the fundamentals first.

**Question 2:** The list of anaerobic byproducts was missing classic fermentation products like ethanol and butyrate. Why?

* **Answer:** The speaker speculates that this is a key feature of the "typicality" approach. Secretion of molecules like ethanol is often an *optimal* strategy for redox balance. The secretions in his random models arise from "metabolic imbalances" and suboptimal pathway usage, not from an optimized strategy. Therefore, the model produces a different, more stochastic set of byproducts.

**Question 3:** How realistic are the actual metabolic pathways in these random models?

* **Answer:** From a stoichiometric and topological perspective, the pathways are valid and "make sense." Some are unusual but possible. The speaker views this as an opportunity to add *more* realism in the future by layering on additional constraints, such as thermodynamics, to further refine the space of possible networks.

**Question 4 (Key Question):** Do you really need the complexity of metabolic networks? Could you get the same result with a simpler model of random interactions, like a **Lotka-Volterra** model?

* **Answer:** This is the critical question. The speaker's answer is **no**. They have tried using standard Lotka-Volterra models (which use randomized interaction coefficients) and they **do not** reproduce the key finding of emergent competitive exclusion in pairwise tests. This implies that the structure of metabolic networks imposes a fundamental, non-random constraint on the *types* of interactions that can occur. The "randomness" is not in the interactions themselves, but in the network topology that generates them, and this distinction is crucial. He is still working to fully explain why this is the case.

---

## 4. Comprehensive Summary

* **Motivation:** The field of microbial ecology lacks a strong theoretical framework that can both generate general principles and make specific, data-driven predictions. Abstract models are too generic, while standard metabolic models are too rigid in their assumption of optimality. This research aims to create a "middle way" to bridge this gap.

* **Research Question / Central Argument:** Can we derive fundamental principles of microbial community structure and dynamics by studying the collective behavior of "typical," randomly generated, suboptimal metabolisms? The central argument is that this "random biology" approach is a powerful new lens that can reveal emergent ecological patterns that are otherwise difficult to explain.

* **Conclusion:** The study concludes that the random metabolism approach is remarkably successful. It generates organisms with realistic "leaky" phenotypes and assembles them into communities whose structure (e.g., reliance on cross-feeding, emergence of a rare biosphere) mirrors real ecosystems. Most importantly, this framework successfully reproduced a counter-intuitive experimental result—that members of a stable community often fail to coexist in pairs—which simpler models like Lotka-Volterra cannot. This suggests that the very structure of metabolic networks imposes fundamental, non-random constraints on ecological interactions.

* **Current Limitations:** The primary limitation is that the work is still in progress. As the speaker admits, they do not yet fully understand the precise mechanism that leads to the emergent pairwise competition. The model is also currently limited to a single carbon source (glucose) and does not yet include other important biological constraints like thermodynamics.

* **Alternative Perspectives:** The main alternative is the traditional approach: painstakingly building accurate, curated metabolic models for real species and simulating their interactions. While this is essential for studying specific systems, the speaker's argument is that this approach can miss general principles that are not specific to any one organism but are properties of metabolic network topology itself.

* **Potential Next Steps:**
    1. **Uncover the Mechanism:** The most pressing next step is to figure out *why* the random metabolic models lead to emergent competitive exclusion in pairwise culture.
    2. **Add More Constraints:** Incorporate additional layers of biological reality into the model generation process, such as thermodynamic constraints, to further refine the space of "possible" metabolisms.
    3. **Explore More Environments:** Expand the simulations to include more complex environments with multiple carbon sources to see how niche partitioning and resource competition evolve.
    4. **Connect to Real Data:** Attempt to parameterize the random generation process using large-scale genomic datasets to see if it can be biased towards generating communities that look like those from a specific environment (e.g., the gut vs. soil).
