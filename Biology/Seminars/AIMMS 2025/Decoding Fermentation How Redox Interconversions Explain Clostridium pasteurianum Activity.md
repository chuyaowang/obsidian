# Decoding Fermentation: How Redox Interconversions Explain *Clostridium pasteurianum* Activity

**Speaker:** Wessel de Kok
**Affiliation:** Technische Universiteit Delft
**Event:** AIMMS Symposium 2025
#seminar 

---

## Executive Summary

This talk presents a mechanistic explanation for metabolic pathway selection in *Clostridium pasteurianum*, an obligate anaerobic bacterium. De Kok argues that fermentative organisms cannot decouple anabolic and catabolic pathways because their strict requirement to internally balance redox cofactors (NADH, NADPH, and ferredoxin) constrains the product spectrum. The key insight is that electron bifurcation enables *C. pasteurianum* to harvest ~11% extra ATP during fermentation, and that ferredoxin electrons are redirected into biomass synthesis rather than released as hydrogen — a form of energy conservation not based on ATP. This framework, formalized as a flux balance analysis (FBA) model, successfully predicts the organism's growth-rate-dependent product spectrum.

---

## 1. Motivation: Why Fermentation Pathway Selection Remains Poorly Understood

Fermentations drive anaerobic digestion, wastewater treatment, and numerous industrial biotechnological processes. Despite this, the rules governing how fermentative organisms choose their active metabolic routes are incompletely understood. De Kok emphasizes this paradox: *C. pasteurianum* is a relatively simple microbe with well-characterized pathways, yet its product spectrum resists straightforward prediction.

Two guiding principles frame the entire presentation:

1. **Thermodynamics**: Fermentations operate much closer to thermodynamic equilibrium than respiration. Organisms must employ creative mechanisms — such as electron bifurcation — to extract extra energy from substrate.
2. **Redox cofactor balance**: Without a respiratory chain to accept NADH, fermentative organisms must internally balance all redox carriers. This constraint fundamentally restricts the feasible product spectrum.

*C. pasteurianum* was chosen as a model because it is dominant in anaerobic communities, isolatable in the laboratory, capable of using many substrates, and — even on glucose alone — produces a broad product spectrum, making it ideal for studying metabolic regulation. Decades of literature provide a data foundation for hypothesis testing.

---

## 2. Theoretical Framework: Electron Carriers and the Product Spectrum

### 2.1 Five Fermentation Products and Their Redox Implications

When fermenting glucose via the Embden-Meyerhof-Parnas (EMP) glycolysis, *C. pasteurianum* can produce five endpoint products, categorized by their net effect on NADH balance:

- **Lactate**: Pyruvate is the internal electron acceptor. NADH-neutral — no redox management needed.
- **Acetate**: Generates extra ATP but produces no NADH sink, so complementary products must rebalance.
- **Butyrate**: Consumes acetyl-CoA units; generates extra ATP. Does not consume NADH.
- **Ethanol**: Reduces acetaldehyde; consumes NADH. Acts as an electron sink.
- **Butanol**: Highly reduced; consumes NADH.

Thus, acetate production must always be accompanied by a product that net accepts NADH. The three candidates — ethanol, butanol, and butyrate — ensure redox neutrality.

### 2.2 Three Redox Carriers With Distinct Roles

*C. pasteurianum* uses three electron carriers:

- **Ferredoxin**: An exceptionally potent electron donor. Crucially, it is the *only* carrier that can transfer electrons to protons to produce H₂ gas. Because H₂ can be released into the environment, ferredoxin does **not** need to be internally balanced — it serves as a redox "release valve."
- **NADH**: Preferentially used as an electron acceptor in catabolism. Must be internally balanced.
- **NADPH**: Preferentially used as an electron donor in anabolism (biosynthesis). Must be internally balanced.

This separation of roles — NADPH for building, NADH for breaking down — is essential for maintaining thermodynamic feasibility across reactions simultaneously. A critical consequence is that **direct electron transfer from NADH to ferredoxin is thermodynamically infeasible**: the reduction potential difference makes the reaction energetically uphill.

---

## 3. The Mechanism of Electron Bifurcation

### 3.1 Principle

Electron bifurcation couples an energetically unfavorable reaction to a favorable one, allowing both to proceed simultaneously as long as the overall reaction is thermodynamically feasible. In *C. pasteurianum*, this mechanism enables effective NADH-to-ferredoxin electron transfer.

### 3.2 Quantitative Energy Advantage

- **Without electron bifurcation**: maximum yield of ~3 ATP per glucose.
- **With electron bifurcation** and an equimolar (1:1) acetate-to-butyrate product ratio: yield increases by approximately **11%**, reaching ~3.33 ATP per glucose.

This extra ATP comes from coupling the endergonic oxidation of NADH by ferredoxin with the exergonic reduction of ferredoxin-coupled reactions during butyrate synthesis.

### 3.3 The Predicted vs. Observed Paradox

Theory therefore predicts that *C. pasteurianum* should produce a 1:1 acetate-to-butyrate ratio under optimal conditions. De Kok reviewed **30 years of literature experiments** across diverse growth conditions and found that **no study reports this ratio in practice**. This discrepancy is the central puzzle of the presentation.

---

## 4. Growth-Dependent Metabolic Shifts: Anabolism as the Missing Variable

### 4.1 Chemostat Evidence

A previous master's student, Daniela Verbonne, grew *C. pasteurianum* in a chemostat at three dilution rates (low, medium, high) and measured the fermentation product spectrum. Key observation: **the butyrate-to-acetate ratio increases with increasing growth rate**, diverging progressively from the theoretical 1:1 prediction.

### 4.2 Why: The Anabolic Redox Imbalance

The explanation lies in **anabolic precursor synthesis**. All cellular biomolecules — proteins, DNA, RNA, lipids — require carbon skeletons derived from catabolic intermediates. When acetyl-CoA is channeled into fatty acid synthesis, NADH is released but NADPH is required. This creates a cofactor mismatch.

- Catabolism of glucose → releases NADH
- Anabolic biosynthesis (lipids, proteins, nucleic acids) → releases NADH but requires NADPH
- These two carriers cannot be directly interconverted in *C. pasteurianum*

The higher the growth rate, the more biomass must be synthesized, and the greater the excess NADH generated by anabolic pathways. This additional NADH must be rebalanced by catabolism — specifically, by producing more butyrate (a more NADH-consuming product than acetate). This shifts the ratio away from 1:1 at high growth rates.

### 4.3 Solving the NADPH Deficit

*C. pasteurianum* lacks the oxidative pentose phosphate pathway, the standard NADPH-generating route in other organisms. Alternative pathways each cost ~1 ATP per NADPH — too expensive in a fermentative energy budget. The solution: **ferredoxin-to-NADP electron transfer**. Ferredoxin carries electrons of extremely low reduction potential; transferring them to NADP⁺ to generate NADPH is thermodynamically feasible and was experimentally demonstrated as early as 1979.

This means that instead of releasing ferredoxin electrons into the environment as H₂, the organism redirects them into biomass. This is a form of **energy conservation independent of ATP**: retaining low-potential electrons in the biological system avoids the cost of regenerating them later.

---

## 5. Summary of the Metabolic Logic

At **low growth rates** (maintenance-dominated):
- Minimal biosynthesis → minimal excess NADH from anabolism
- Ferredoxin can serve mostly as a release valve
- Product spectrum approximates the 1:1 acetate-butyrate ratio

At **high growth rates** (growth-dominated):
- Substantial biosynthesis → large excess NADH
- More butyrate must be produced to rebalance catabolism
- Ferredoxin is increasingly redirected to NADPH for anabolism
- Observed butyrate-to-acetate ratio diverges above 1:1

---

## 6. Flux Balance Analysis Model

De Kok developed a simple FBA model (implemented in COBRApy) containing all fermentative routes, anabolic precursor generation, and a biomass equation. Key results:

- **Product spectrum predictions** match experimental data remarkably well, including the growth-rate-dependent shift in butyrate-to-acetate ratio
- **Hydrogen production** remains the one outlier: the model cannot accurately fit measured H₂ rates, suggesting missing mechanisms (possibly hydrogen overpressure effects or uncharacterized regulatory steps)

The model's success validates the theoretical framework. The limitation in predicting hydrogen production motivates additional targeted experiments.

---

## 7. Q&A

**Q: What is the enzymatic mechanism for ferredoxin-to-NADP transfer, and why aren't alternative NADPH pathways used?**
The ferredoxin:NADP oxidoreductase enzyme was experimentally characterized in 1979. Alternative routes (malic enzyme, transhydrogenase) each cost ~1 ATP per NADPH — too energetically costly given fermentation's tight energy budget. The oxidative pentose phosphate pathway is completely absent from the genome.

**Q: Could thermodynamic constraints (ΔG values) be incorporated into the FBA model?**
Currently, no thermodynamic constraints are included because the basic metabolic pattern is preserved across conditions. At higher dilution rates, increased formate production may reflect hydrogen overpressure thermodynamically redirecting ferredoxin flux. This is an active research question in a related group.

**Q: Is hydrogen overpressure the explanation for the poor hydrogen fit?**
Plausible but unconfirmed. The overall model fit is good; hydrogen is the outstanding outlier. New experiments are being designed to investigate.

---

## 8. Comprehensive Summary

### Central Argument
Metabolic pathway selection in *C. pasteurianum* is governed by the interaction of two thermodynamic constraints: the need to conserve energy via electron bifurcation, and the need to balance all redox cofactors across both catabolic and anabolic reactions. The growth rate determines how much biosynthesis occurs, which in turn alters the NADH demand from catabolism, explaining why the experimental product spectrum deviates from the thermodynamically optimal prediction at high growth rates.

### Broader Implication
In aerobic organisms, anabolism and catabolism can be coupled primarily via ATP. In fermentative organisms, **redox balance adds a second mandatory coupling** between the two: whatever the anabolism generates or consumes in terms of redox cofactors must be compensated by catabolism. This insight is critical for understanding and engineering anaerobic fermentations.

### Limitations
- Hydrogen production is not yet accurately modeled
- The model is relatively simple and may not capture regulatory or kinetic details
- Focused on glucose; other substrates may introduce additional complexity

### Potential Next Steps
- Experiments at controlled hydrogen partial pressures to isolate overpressure effects
- Dynamic modeling to capture transient behavior
- Extension to other anaerobic organisms and mixed-substrate conditions
- Isotope labeling experiments to directly confirm predicted cofactor imbalances

---

*Transcript corrections: "Vessel" → Wessel; "paradoxin" → ferredoxin; "uterate" → butyrate; "ETG" → ATP; "pirotate" → pyruvate; "echo model ratio" → equimolar ratio.*
