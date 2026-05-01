# Dual Substrate Uptake can Release Metabolic Limitations Leading to Improved Synergistic Yields: Metabolic Interactions between Different Substrates

**Speaker:** Timmy Paez-Watson, Technische Universiteit Delft (TU Delft)
**Event:** Amsterdam Institute of Molecular and Life Sciences (AIMMS) Symposium
**Transcribed Text:** `talk2.txt`
#seminar

---

## Contextual Knowledge (Key Concepts)

* **Polyphosphate-Accumulating Organisms (PAOs):** A functional group of bacteria, not a single species, that are central to Enhanced Biological Phosphorus Removal (EBPR) in wastewater treatment. Their defining characteristic is their ability to store large amounts of phosphorus as intracellular polyphosphate granules.
* **Polyhydroxyalkanoates (PHAs):** A class of biodegradable biopolyesters produced by many bacteria as intracellular carbon and energy storage granules. PAOs synthesize PHAs (like PHB) under anaerobic conditions.
* **Glycogen:** A branched polymer of glucose that serves as a form of energy and carbon storage in animals, fungi, and many bacteria, including PAOs.
* **Dynamic Flux Balance Analysis (dFBA):** An extension of standard FBA used to simulate the metabolic behavior of an organism over time. It is essential for systems like PAOs where the metabolic objective (growth) is achieved over a long period and involves distinct metabolic modes (e.g., anaerobic storage, aerobic growth).
* **Anaplerotic Reactions:** Metabolic reactions that replenish the intermediates of a central metabolic pathway, such as the TCA cycle. In the talk, when aspartate is the sole carbon source, anaplerotic reactions are needed to form other essential precursors, which can be inefficient.
* **Metabolic Synergy:** An interaction where the combined effect of two or more factors (in this case, substrates) is greater than the sum of their individual effects. The talk demonstrates a clear case of synergy where the co-utilization of two substrates leads to a higher growth yield than would be expected from a simple average.

---

## 1. Overview and Logical Flow of the Talk

This talk explores the complex metabolic strategies of specialized bacteria in wastewater treatment plants. The speaker, Timmy Paez-Watson, explains how these microbes use a unique storage-based metabolism to survive in cyclical, feast-famine environments. The core of the presentation is the discovery, through metabolic modeling and experimental validation, that feeding these bacteria a *combination* of substrates can unlock synergistic effects, releasing metabolic bottlenecks and leading to more efficient growth.

The logical flow of the presentation is as follows:

1. **Introduction:** Setting the scene with microbes living in dynamic, cyclical environments, using wastewater treatment plants as a prime example.
2. **The Biological System:** Introducing **Polyphosphate-Accumulating Organisms (PAOs)** and their feast-famine survival strategy, which involves storing carbon (as PHAs) and energy/reducing power (as polyphosphate and glycogen).
3. **The Problem:** Highlighting the metabolic inefficiency of this strategy, particularly the energy cost of the "futile cycle" of glycogen synthesis and degradation, which results in very slow growth.
4. **The Research Question:** Posing the central question: Can the co-uptake of a second substrate alongside the primary one (acetate) provide the necessary metabolic components (specifically NADH) to bypass the inefficient glycogen cycle?
5. **The Modeling Approach:** Explaining the use of a specialized **dynamic Flux Balance Analysis (dFBA)** to simulate the PAOs' metabolism over a full anaerobic-aerobic cycle, allowing for the optimization of growth yield over time.
6. **Modeling Results & The Synergy Mechanism:** Presenting the key modeling discovery—a synergistic interaction between acetate and aspartate. The model predicted that their combined uptake leads to a higher growth yield than expected. The mechanism is a "bi-directional synergy" where each substrate's metabolism provides what the other is missing, simultaneously removing the bottlenecks of both pathways.
7. **Experimental Validation:** Showing data from bioreactor experiments that confirmed the model's central mechanistic prediction: co-feeding acetate and aspartate significantly reduced or eliminated the anaerobic consumption of glycogen.
8. **Conclusion & Q&A:** Concluding that these synergistic interactions are not unique and are highly relevant for designing more efficient bioprocesses, followed by a Q&A session clarifying details about the yield gain, higher-order interactions, and phosphate uptake affinity.

***Note on Transcription:*** *The provided text was machine-transcribed and contained several errors. These have been interpreted and corrected for clarity in this summary. For example, "POWs" has been corrected to **PAOs**, "THB" to **PHB**, "aparotic roots" to **anaplerotic routes**, and "wastewater-deuterium plants" to **wastewater treatment plants**.*

---

## 2. Sectional Summaries

### 2.1 Introduction: Microbes in Cyclical Environments

* **Challenge Resolved:** To frame the research in a relevant ecological context. The speaker establishes that microbes in nature, and specifically in engineered systems like wastewater treatment plants, live in highly dynamic and cyclical conditions (e.g., anaerobic phase followed by aerobic phase).
* **Methods Used:** The talk uses the example of an activated sludge wastewater treatment plant, where microbial communities are cycled through different tanks (anaerobic/aerobic) to remove nutrients.
* **Results:** This cycling process is described as an engineered strategy that enriches for specific microorganisms with astonishing storage capacities.
* **Leads to Next Section:** This sets the stage for introducing the specific type of microorganism that thrives in these conditions: the Polyphosphate-Accumulating Organism (PAO).

### 2.2 The Biological System: Polyphosphate-Accumulating Organisms (PAOs)

* **Challenge Resolved:** To explain the complex survival strategy of PAOs.
* **Methods Used:** The speaker details the PAO's metabolism across the anaerobic-aerobic cycle.
  * **Anaerobic (Feast):** In the absence of an external electron acceptor (like oxygen), PAOs take up abundant carbon sources (like acetate) and store them as **Polyhydroxyalkanoates (PHAs)**, a type of bioplastic. This process requires energy (ATP) and reducing power (NADH).
  * **Energy Source:** To fuel this uptake, they break down internal storage polymers: **polyphosphate** for ATP and **glycogen** for both ATP and NADH. This allows them to "kidnap" the available food source from competitors.
  * **Aerobic (Famine):** In the next phase, with oxygen available, they oxidize the stored PHA. This generates a large amount of resources, which they use to grow and, critically, to replenish their internal stores of polyphosphate and glycogen for the next cycle.
* **Results:** This is presented as a highly effective competitive strategy in feast-famine environments.
* **Leads to Next Section:** The speaker points out a major drawback to this strategy: its inefficiency, which is the central problem the research aims to solve.

### 2.3 The Problem: The Inefficiency of Glycogen Cycling

* **Challenge Resolved:** To identify the key limitation of the PAO metabolic strategy.
* **Methods Used:** The speaker identifies the degradation of glycogen in the anaerobic phase and its re-synthesis in the aerobic phase as a **futile cycle**. While temporally separated, it represents a net loss of ATP and is metabolically expensive.
* **Results:** This inefficiency is the reason PAOs are very slow-growing organisms, with duplication times of several days. This slow growth is a major limiting factor.
* **Leads to Next Section:** This leads directly to the research question: can this inefficiency be overcome?

### 2.4 The Research Question & Hypothesis

* **Challenge Resolved:** To formulate a testable hypothesis to address the problem of PAO inefficiency.
* **Methods Used:** The core idea proposed is to release the dependence on glycogen. The hypothesis is that if PAOs are fed a second substrate along with acetate, this co-substrate could potentially provide the NADH required for PHA synthesis directly.
* **Results:** This would eliminate the need to break down glycogen, breaking the futile cycle and potentially leading to more efficient growth. The study sets out to explore this hypothesis using metabolic modeling.
* **Leads to Next Section:** To test this, a standard modeling approach won't work. A specialized method is needed to simulate the cyclical nature of the PAO's life, which is introduced next.

### 2.5 The Modeling Approach: Dynamic Flux Balance Analysis (dFBA)

* **Challenge Resolved:** To choose a modeling framework capable of simulating a microbe whose metabolic objective (growth) is decoupled from its immediate substrate uptake and is realized over a full cycle.
* **Methods Used:** The speaker used a simple metabolic model (glycolysis, TCA cycle, anaplerotic routes) and a specialized technique called **conditional Flux Balance Analysis**. This is a form of dynamic FBA where the objective function (e.g., maximize biomass yield) is not applied at each instant but is optimized over the entire cycle, subject to the constraints of each phase (anaerobic/aerobic).
* **Results:** This powerful method allows the model to capture the dynamic storage-based strategy of PAOs. The model was then used to simulate the co-uptake of acetate with various other potential substrates (Substrate X) to see if growth yields could be improved.
* **Leads to Next Section:** This sets up the presentation of the modeling results, where the concepts of additive vs. synergistic effects are explained.

### 2.6 Modeling Results: The Discovery of Bi-Directional Synergy

* **Challenge Resolved:** To analyze and interpret the results of the dFBA simulations.
* **Methods Used:** The speaker presents a schematic to explain metabolic interactions. If two substrates have no interaction, the yield of a mixture should be the weighted average of the individual yields (an "additive" line). Deviations from this line indicate synergy (higher yield) or antagonism (lower yield).
* **Results:** The simulation of co-feeding **acetate and aspartate** showed a strong positive deviation, indicating a powerful synergistic interaction that led to a higher growth yield than either substrate alone could achieve at its best.
* **Leads to Next Section:** The model predicts synergy. The next step is to use the model to understand the underlying mechanism.

### 2.7 The Mechanism: Releasing Reciprocal Limitations

* **Challenge Resolved:** To explain *why* acetate and aspartate uptake is synergistic.
* **Methods Used:** By inspecting the flux distributions in the model at different substrate ratios, the speaker identified the specific metabolic bottlenecks for each substrate when used alone.
  * **Acetate-only limitation:** The need to break down glycogen to get NADH for PHA synthesis.
  * **Aspartate-only limitation:** The need to use energy-inefficient anaplerotic routes to convert aspartate into the acetyl-CoA pathway.
* **Results:** When fed together, these limitations are mutually resolved. Aspartate metabolism naturally produces the NADH that acetate uptake requires, eliminating the need for glycogen. Simultaneously, the acetate fed directly into the TCA cycle bypasses the need for the inefficient anaplerotic conversion of aspartate. This "bi-directional synergy" is the source of the improved yield.
* **Leads to Next Section:** With a clear mechanistic prediction from the model, the final step is to test it in a real biological system.

### 2.8 Experimental Validation and Conclusion

* **Challenge Resolved:** To experimentally validate the key mechanistic prediction from the metabolic model.
* **Methods Used:** An enriched PAO culture in a bioreactor was fed different substrate mixtures anaerobically. The consumption of internal glycogen stores was measured.
* **Results:** The experimental data perfectly matched the model's prediction. When fed acetate alone, glycogen was consumed. When fed a mix of acetate and aspartate, glycogen consumption was lower. When fed aspartate alone, no glycogen was consumed. This provided strong evidence for the proposed synergistic mechanism. The speaker concludes that such interactions are likely common for many substrates, which is highly relevant for the complex "soup" found in real wastewater, and this knowledge can be used to design more efficient bioprocesses.

---

## 3. Summary of the Q&A Session

**Question 1:** The predicted biomass yield gain in the model seems very small. How can such a tiny difference be meaningful in a real bioreactor?

* **Answer:** The yield gain shown is for a single anaerobic-aerobic cycle, which only represents about 1/30th of the organism's total duplication time. This small but positive gain accumulates over many cycles. Over the full lifetime of the organism, this can translate into a significant competitive advantage, for example, by reducing the total duplication time from four days to three.

**Question 2:** Is it possible to assess higher-order interactions (e.g., with three or more substrates), and is the model suitable for that?

* **Answer:** Yes, the model is perfectly capable of simulating this, and it would be quite easy to do. The speaker notes that he was initially surprised to find any interaction at all, thinking it would be purely additive. He draws a parallel to microbial community interactions, where different species can mutually resolve each other's limitations, suggesting the same principle applies *within* a single cell's metabolism when using multiple substrates.

**Question 3:** The process involves exporting phosphate and later re-importing it from the environment. Does this mean the phosphate uptake transporters must have an extremely high affinity?

* **Answer:** Yes, exactly. The transporters for phosphate uptake have a very high affinity, which is necessary for scavenging it from the medium. Additionally, the bioreactors run at a very high biomass concentration, which also influences the dynamics.

---

## 4. Comprehensive Summary

* **Motivation:** The research is driven by the need to improve the efficiency of biological wastewater treatment. The key organisms involved, PAOs, are effective but grow very slowly due to metabolic inefficiencies, limiting process rates. Understanding and overcoming these limitations could lead to more compact, efficient, and cost-effective treatment plants.

* **Research Question / Central Argument:** The central question is whether the primary metabolic bottleneck in PAOs—an energy-intensive futile cycle involving glycogen—can be overcome by providing a mix of substrates instead of a single one. The argument is that co-substrate uptake can create metabolic synergies within the cell, leading to a more efficient overall metabolism and faster growth.

* **Conclusion:** The research successfully demonstrates, through a combination of predictive modeling and experimental validation, that dual substrate uptake can indeed release metabolic limitations. The co-feeding of acetate and aspartate creates a bi-directional synergy where each substrate's metabolism compensates for the other's deficiencies, removing the need for the inefficient glycogen cycle. This is a powerful proof-of-concept that metabolic interactions are not just additive and that this principle can be exploited to improve bioprocesses.

* **Current Limitations:** The study presented focuses on the mechanistic validation over short-term cycles. The Q&A reveals that directly measuring the final, accumulated yield gain over many days is experimentally challenging due to the organisms' extremely slow growth. The work primarily validates the underlying mechanism (reduced glycogen use) rather than the final outcome (faster growth over weeks).

* **Alternative Perspectives:** The talk focuses on exploiting naturally occurring synergies. An alternative, more engineering-heavy perspective would be to genetically modify PAOs to have a more efficient native metabolism, for example, by engineering pathways that provide NADH more directly during acetate uptake, though this is significantly more complex in a non-model organism within a mixed community.

* **Potential Next Steps:**
    1. **Higher-Order Interactions:** As raised in the Q&A, use the model to explore synergies between three or more substrates, which would more closely mimic the complexity of real wastewater.
    2. **Long-Term Studies:** Design and run long-term chemostat experiments to definitively quantify the cumulative effect of synergy on growth rate and competitive fitness over many generations.
    3. **Process Design:** Apply this knowledge to wastewater treatment process design. For example, one could consider co-dosing industrial wastewater streams (which might be rich in specific amino acids or other co-substrates) with municipal wastewater to enhance nutrient removal efficiency.
    4. **Community Context:** Expand the model to include competing organisms (like Glycogen-Accumulating Organisms, GAOs) to see how these synergistic effects alter the competitive landscape of the entire microbial community.
