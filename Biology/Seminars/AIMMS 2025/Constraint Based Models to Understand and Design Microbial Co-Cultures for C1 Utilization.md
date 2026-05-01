# Constraint Based Models to Understand and Design Microbial Co-Cultures for C1 Utilization

**Speaker:** Maria Suarez Diez, Wageningen University & Research
**Event:** Amsterdam Institute of Molecular and Life Sciences (AIMMS) Symposium
**Transcribed Text:** `talk1.txt`
#seminar 

---
## Contextual Knowledge (Key Concepts)

* **Constraint-Based Modeling (CBM):** A mathematical approach to analyze metabolism. Instead of simulating dynamics with kinetic parameters (which are often unknown), it defines the *space of all possible steady-state behaviors* given a set of constraints (thermodynamics, mass balance, nutrient availability).
* **Genome-Scale Metabolic Model (GEM):** The network reconstruction used in CBM, representing all known metabolic reactions in an organism, derived from its annotated genome.
* **Syngas (Synthesis Gas):** A fuel gas mixture consisting primarily of hydrogen (H2), carbon monoxide (CO), and carbon dioxide (CO2). It can be produced from the gasification of carbon-containing materials like biomass or municipal waste.
* **Acetogens:** A group of anaerobic bacteria that can produce acetate (a C2 compound) from C1 compounds (like CO2 or CO) via the Wood-Ljungdahl pathway.
* **Wood-Ljungdahl Pathway:** A metabolic pathway used by acetogens to fix carbon. It is notable for being linear (not a cycle) and highly energy-efficient in terms of carbon, but it yields very little ATP.
* **Electron Bifurcation:** A fundamental energy conservation mechanism in anaerobes. It couples an energetically favorable redox reaction with an unfavorable one, allowing the cell to generate reduced cofactors with higher energy or to create an ion gradient for ATP synthesis from reactions that would otherwise be insufficient.
* **Chemostat:** A laboratory bioreactor where fresh medium is continuously added while culture liquid is continuously removed. At steady state, the microbial growth rate equals the dilution rate, allowing for the study of microbes under constant conditions.
* **Syntrophy:** A metabolic partnership where two or more different microbial species cooperate to carry out a metabolic process that neither can do alone. In this talk, the acetogen produces food for the chain elongator.

---

## 1. Overview and Logical Flow of the Talk

This talk presents a research journey focused on upgrading low-value C1 gases (syngas) into valuable chemicals using multi-species microbial communities. The speaker, Maria Suarez Diez, expertly weaves together concepts from systems biology, metabolic modeling, and experimental microbiology to explain how these complex biological systems can be understood and engineered.

The logical flow of the presentation is as follows:

1. **Introduction:** An overview of the main take-home messages.
2. **Primer on Constraint-Based Modeling:** A brief, accessible explanation of Genome-Scale Metabolic Models (GEMs) for a general scientific audience.
3. **The Societal Challenge & Biological Solution:** Framing the problem of waste valorization and introducing acetogenic bacteria as key players for converting C1 gases.
4. **Deep Dive into Acetogen Metabolism:** Explaining the unique and highly efficient energy conservation mechanism (electron bifurcation) that allows these microbes to live on the "bioenergetic edge."
5. **Designing a Co-culture:** Moving from a single microbe to a two-species co-culture to elongate the initial products into more valuable, longer-chain fatty acids.
6. **The Modeling Challenge:** Detailing the complexities of building a multi-species metabolic model, emphasizing the critical importance of units and relative biomass abundances.
7. **Expanding to a Triculture:** Introducing a third microbe to diversify the product portfolio to include odd-chain fatty acids.
8. **Modeling and Experimental Validation:** Presenting model predictions for the triculture's feasibility and showing the "partial success" of experimental efforts, which confirmed product formation.
9. **Conclusion:** A summary reiterating the key findings and the power of using constraint-based modeling for these energetically-limited systems.

***Note on Transcription:*** *The provided text was machine-transcribed and contained several errors. These have been interpreted and corrected for clarity in this summary. For example, "signals" has been corrected to **syngas**, "acetylides" to **acetogens**, "electrodification" to **electron bifurcation**, and microbial names like "presidium" to **Clostridium**.*

---

## 2. Sectional Summaries

### 2.1 Introduction: Take-Home Messages

The talk begins by clearly stating its core arguments:

* **Challenge:** Syngas, a mixture of CO2 and hydrogen, is a low-value byproduct of waste gasification that can be upgraded.
* **Method:** Microbial co-cultures, centered around acetogenic bacteria, are a promising way to perform this upgrade.
* **Mechanism:** Acetogens convert syngas to acetyl-CoA. These organisms operate at the very limit of thermodynamic feasibility (the "bioenergetic edge"), using the **ion motive force (IMF)** to generate energy where traditional methods are not possible.
* **Modeling:** Because their metabolism is so energetically constrained, **constraint-based modeling (CBM)** is an exceptionally well-suited tool to study them.
* **Difficulty:** Modeling and experimenting with co-cultures is challenging but achievable.

### 2.2 Primer on Genome-Scale Metabolic Models (GEMs)

* **Challenge Resolved:** To make the talk accessible, the speaker first explains what a GEM is.
* **Methods Used:** A GEM is described as a comprehensive "accounting" of all possible metabolic reactions an organism can perform, based on its genomic information. By applying constraints (like nutrient uptake rates) and an objective function (like maximizing growth), these models can predict metabolic phenotypes (e.g., growth rates, product secretion rates).
* **Results:** This framework allows researchers to perform *in silico* calculations to understand how an organism will behave under different conditions.
* **Leads to Next Section:** This introduction establishes the primary tool (GEMs) that will be used to analyze the complex microbial systems discussed next.

### 2.3 The Problem: Upgrading C1 Syngas with Acetogens

* **Challenge Resolved:** Addressing the societal need for a circular economy by finding ways to convert carbon-rich waste into valuable chemicals.
* **Methods Used:** The proposed route is the gasification of waste into **syngas** (CO, CO2, H2). The biological method involves using **acetogenic bacteria** (e.g., *Clostridium autoethanogenum*).
* **Results:** These bacteria utilize the **Wood-Ljungdahl pathway** to convert C1 gases into **acetyl-CoA**, a central metabolic building block. This forms the basis of the proposed bioprocess.
* **Leads to Next Section:** The Wood-Ljungdahl pathway is energetically poor, raising the question of how these organisms survive, which is addressed in the next section.

### 2.4 The Bioenergetic Edge: Acetogen Energy Metabolism

* **Challenge Resolved:** Explaining how acetogens can grow when their core metabolic pathway does not generate ATP through standard substrate-level phosphorylation.
* **Methods Used:** The speaker explains the concept of **electron bifurcation**. This is a sophisticated mechanism where the energy from a favorable redox reaction is used to drive a less favorable one, while simultaneously pumping ions (protons) across the cell membrane.
* **Results:** This process generates an **ion motive force (IMF)**. The flow of these ions back into the cell through an ATP synthase complex is what ultimately generates the organism's energy (ATP). This allows them to "save" small packets of energy that would otherwise be lost as heat. Because they are so limited, their metabolic network is simple, making them ideal candidates for constraint-based modeling, as there are few alternative pathways to consider.
* **Leads to Next Section:** While acetogens can grow on syngas, they produce low-value products like acetate and ethanol. The next logical step is to find a way to upgrade these products.

### 2.5 A Partnership for Value: The Two-Species Co-Culture

* **Challenge Resolved:** To convert the acetate and ethanol from the acetogen into higher-value, longer-chain fatty acids (e.g., butyrate, caproate).
* **Methods Used:** A second species, a **chain-elongating bacterium** like *Clostridium kluyveri*, is introduced. This organism performs **reverse beta-oxidation**, using acetate and ethanol as substrates to build longer carbon chains. A stable **chemostat** (a continuous culture system) was established with both organisms.
* **Results:** Experimental data from the chemostat showed that the two species could coexist syntrophically. The acetogen (*Clostridium autoethanogenum*) produced acetate, which was then consumed by the elongator (*C. kluyveri*) to produce butyrate and caproate, successfully upgrading the product.
* **Leads to Next Section:** With experimental proof-of-concept, the next challenge is to model this two-species community to understand it better.

### 2.6 Modeling the Co-Culture: Units and Abundances

* **Challenge Resolved:** Building a predictive multi-species metabolic model is not as simple as combining two individual GEMs. The main challenge is reconciling the units.
* **Methods Used:** Individual models use specific fluxes (e.g., mmol/gDW/hr, where gDW is grams of dry weight of that specific organism). In a community, fluxes must be expressed in environmental terms (e.g., mmol/L/hr) to be comparable. This requires explicitly modeling the **relative biomass abundance** of each species. The speaker highlights that cell counts (from experiments) must be converted to biomass fractions for the model, as cell sizes can differ dramatically.
* **Results:** A multi-species model was created that accounts for the shared environment and the biomass ratio of the two organisms. The model showed that the predicted product profile is highly sensitive to the relative abundances of the species. The model's predictions were successfully matched with the experimental data.
* **Leads to Next Section:** The two-species system is limited to producing even-numbered carbon chains. To create a more diverse product range, the system must be expanded.

### 2.7 The Triculture: Adding Odd-Chain Production

* **Challenge Resolved:** To produce odd-chain fatty acids (e.g., propionate, valerate), which are also valuable chemicals.
* **Methods Used:** A third organism, ***Anaerotignum neopropionicum***, was added to the co-culture. This bacterium can produce propionate, which can then be used by the chain elongator as a primer to create odd-chain fatty acids.
* **Results:** The model was expanded to three species. It was used to perform a broad exploration of the solution space, predicting the ranges of dilution rates and species proportions where a stable triculture would be feasible. This *in silico* screening provides a map to guide difficult and time-consuming experimental work.
* **Leads to Next Section:** The final step is to test these model predictions in the lab.

### 2.8 Triculture Experiments: A Partial Success

* **Challenge Resolved:** To experimentally validate the feasibility of the three-species co-culture.
* **Methods Used:** Chemostat and batch-like experiments were conducted with all three microbes.
* **Results:** This proved to be operationally very difficult. A stable, continuous three-species chemostat was **not achieved**. However, the speaker calls it a "partial success" because in batch-like systems, they could confirm the presence of all three species and, crucially, they detected the production of the **full range of both odd- and even-chain fatty acids**. This confirmed that the designed metabolic handoffs were possible, even if stabilizing the community long-term remains a challenge.

---

## 3. Comprehensive Summary

* **Motivation:** The research is driven by the need for a sustainable circular economy. It aims to valorize carbon-rich waste streams by converting them into valuable chemicals, reducing reliance on fossil fuels and mitigating waste accumulation. The specific route explored is the bioconversion of syngas, a product of waste gasification.

* **Research Question / Central Argument:** The central argument is that complex, syntrophic microbial co-cultures can be rationally designed and understood to upgrade C1 gases into a diverse portfolio of valuable fatty acids. The core hypothesis is that constraint-based metabolic modeling is an essential tool for this task, especially because the chosen organisms are severely limited by their energy metabolism, making their behavior more predictable.

* **Conclusion:** The research successfully demonstrated that co-cultures of acetogens and chain-elongating bacteria can effectively convert syngas into valuable even- and odd-chain fatty acids. The speaker concludes that:
    1. These systems are thermodynamically feasible but operate at the very edge of what is possible, relying on sophisticated energy conservation mechanisms like electron bifurcation.
    2. Constraint-based modeling is a powerful and appropriate tool for these systems, allowing for the exploration of feasible operating conditions and providing key insights into their metabolism.
    3. Modeling multi-species communities requires careful handling of biological and mathematical formalisms, particularly the relative biomass abundances of the constituent species.
    4. While experimentally challenging, the designed metabolic pathways were validated, confirming the production of the target chemicals.

* **Current Limitations:** The primary limitation is experimental. While the metabolic potential of the triculture was confirmed, achieving a stable, continuous culture in a chemostat proved to be very difficult. This highlights the gap that can exist between what is metabolically possible (*in silico* prediction) and what is operationally stable in a dynamic, multi-species biological system.

* **Alternative Perspectives:** The talk focuses exclusively on syntrophic co-cultures. An alternative approach, not discussed, would be to use metabolic engineering to consolidate all the desired pathways into a single, robust host organism. This would eliminate the complexities of managing inter-species interactions but would present its own significant genetic engineering challenges, especially in non-model organisms.

* **Potential Next Steps:**
    1. **Stabilize the Triculture:** The immediate next step is to continue working towards establishing a stable, continuous chemostat of the three-species community. This may involve fine-tuning media composition, dilution rates, or reactor conditions.
    2. **Dynamic Modeling:** The current constraint-based models assume steady state. Developing dynamic models could help predict how the community composition changes over time and how to avoid washout of one or more species.
    3. **Explore Other Partners:** Search for or engineer other microbial partners with different chain-elongation capabilities or the ability to produce other classes of valuable chemicals from acetate/ethanol.
    4. **Process Optimization:** Use the validated model to optimize the process for yield, titer, and productivity of specific target molecules.
