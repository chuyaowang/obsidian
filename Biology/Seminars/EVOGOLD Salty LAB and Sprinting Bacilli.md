# EVOGOLD: Salty LAB and sprinting Bacilli

#seminar 

> Simone and Daniel
> VU General Lab Meeting

## 1. Foundational Context: ALE and the EVOGOLD Motivation

### What is Adaptive Laboratory Evolution (ALE)?

Adaptive Laboratory Evolution (ALE) is a cornerstone of microbiology research where microbial populations are cultured under defined selection pressures for extended periods—often spanning hundreds of days and thousands of generations. By maintaining a continuous growth environment, researchers allow natural selection to identify and enrich for beneficial mutations that optimize cellular fitness for specific environmental stressors (e.g., thermal stress, nutrient limitation, or chemical inhibitors).

### The Evolution of EVOGOLD (Continuous Longitudinal Cultivation)

Traditional ALE systems, such as batch transfers or chemostats, are "well-mixed" environments where nutrients and cells are uniformly distributed. While effective, these systems primarily select for "greedy" bacteria—those with the highest specific growth rate ($\mu_{max}$) or nutrient affinity ($K_s$). They largely ignore spatial colonization and migration efficiency.

The **EVOGOLD** system was developed to move beyond these limitations by introducing a 25-meter "race track" for bacteria. The core research motivations are:

1. **Selection for Spatial Expansion:** Shifting the goal from "who grows fastest in a flask" to "who colonizes new territory most efficiently."
2. **Metabolic Convection Interactions:** Probing how bacteria utilize fluid currents created by their own density-altering metabolism to move through an environment.
3. **High-Throughput Automation:** Replacing labor-intensive manual transfers with a continuous system that can run autonomously for months, reducing contamination risk and human error.

---

## 2. Sectional Report: Evolutionary Dynamics and the "Sprinting" Mechanism (Simone)

### Hardware and Experimental Design

Simone utilized a system of 20–25 meter towers using tubing with an inner diameter of 2–6mm. The system is filled with medium containing a pH indicator and monitored via a custom imaging system that tracks the "front" of the bacterial population as it acidifies the medium.

### The Physics of Metabolic Convection

A primary challenge was explaining how non-motile *Bacillus subtilis* could migrate at several centimeters per hour—a speed far exceeding simple diffusion.

- **The Phenomenon:** As bacteria at the growth front consume glucose, they excrete metabolic byproducts that are lighter than the surrounding medium.
- **The Convective Wave:** This creates density differences that trigger a fluid current: a "forward stream" at the top of the tube and a "back sweep" at the bottom.
- **Computational Validation:** Collaborating with Christian Chioriano (KAUST), fluid dynamics models successfully reproduced these "solitary waves," proving that the bacteria are essentially "surfing" a current of their own creation.

### Genomic Convergence: The GDPP (1816) Hotspot

Across eight independent towers using both glucose and galactose, Simone observed a consistent phenotypic "speedup" after approximately two weeks of cultivation. Sequencing revealed a striking pattern of **convergent evolution**:

- **Gene 1816 (GDPP):** Mutations occurred in this gene across almost all towers. GDPP codes for a phosphodiesterase that breaks down **cyclic-di-AMP**, a critical second messenger regulating osmotic stress and potassium/water uptake.
- **The "Salty" Buoyancy Theory:** While GDPP mutations often hinder growth under high salt, they are beneficial in EVOGOLD because they likely alter cellular density. By modifying potassium transport, cells may become "lighter," allowing them to stay in the forward-moving upper stream longer.
- **Supporting Evidence:** In a 2mm PVC tower experiment, the entire **BusA cluster** (glycine betaine transport) was deleted. Like GDPP, BusA is part of the osmotic stress response, reinforcing that **buoyancy control** is the primary adaptive strategy in this system.

---

## 3. Sectional Report: Motility and the "Fluid Treadmill" (Daniel)

### Challenges and Competition Regimes

Daniel addressed the question of how active swimming (motility) interacts with the passive convective currents discovered by Simone. He compared a Wild Type (GFP-labeled, motile) strain with a **$\Delta$hag mutant** (RFP-labeled, non-motile).

### Key Findings

- **The Cost of Motility:** In aerobic, shaken flasks, non-motile strains won because swimming is an energetically expensive waste when nutrients are uniform.
- **The Oxygen Race:** In closed PVC tubes, motility was a massive advantage. Motile bacteria "sprint" ahead to consume the limited oxygen at the front, effectively starving the non-motile population behind them. In these conditions, motile strains reached nearly **100% frequency**.
- **The Fluid Treadmill Paradox:** A critical observation was that as the tube diameter increased, the net expansion speed of motile bacteria *decreased*. Daniel theorized that as the convective currents become stronger in larger tubes, swimming bacteria might accidentally navigate into the "back-sweep" (the backward current at the bottom), effectively running on a "treadmill" that hinders their forward progress.
- **Permeability Constraints:** PVC has extremely low oxygen permeability. Daniel hypothesized that in oxygen-rich **silicon tubing**, the selective advantage of motility would be diminished, potentially giving non-motile "sprinters" a fairer shot at the race.

---

## 4. Exhaustive Q&A Session Report

### Technical Inquiries and Speaker Responses

1. **Q: How are the number of generations estimated?**
   - **A:** It is complex due to the "contributing pool" effect. We estimate 10–20 generations per meter, totaling roughly 400–2000 over the tower, though modeling is required to be precise.
2. **Q: Don't cells at the bottom move backward?**
   - **A:** Yes. There is a "turnover." Winners are at the front, but cells can rise from the bottom into the forward stream if they change density through metabolism.
3. **Q: Does the model include single-particle tracking?**
   - **A:** Yes, the KAUST team is currently incorporating this to track the specific nutrient/oxygen history of individual cells.
4. **Q: How do you visualize the biomass?**
   - **A:** We use pH indicators (tracking acidification) and light scattering. Fluorescent proteins were not required for the primary speed measurements.
5. **Q: How do you sample the "before" and "after" points?**
   - **A:** By clamping sections of the tube at the end of the run. While the "back" samples are months old and may be non-viable, they are still suitable for sequencing.
6. **Q: Does pipette error multiply exponentially?**
   - **A:** No. A 10% error in the starting inoculum remains a 10% error throughout the experiment.
7. **Q: If you re-inoculate an evolved strain, is it faster?**
   - **A:** Yes. Previous experiments by Jeroen confirmed that evolved strains migrate significantly faster than the parental wild type.
8. **Q: Have you attempted mutation reversion?**
   - **A:** It is a planned control. Reverting the GDPP mutation using classical or CRISPR methods would definitively prove its role in the "speedup."
9. **Q: What is the specific function of cyclic-di-AMP?**
   - **A:** It is a signaling molecule that tells the cell how to handle osmotic stress, specifically regulating potassium uptake.
10. **Q: Why is the GDPP mutation "mysterious" in this system?**
    - **A:** Because the system doesn't use high salt, yet it targets salt-stress genes. The benefit is likely a side-effect on cellular density and buoyancy.
11. **Q: Could this be an adaptation to the CDNPC medium?**
    - **A:** Unlikely, as the same mutation occurs in different media configurations (glucose vs. galactose).
12. **Q: Are the evolved strains faster in pure growth?**
    - **A:** Surprisingly, no. Evolved strains often grow **slower** in flasks than their parents, suggesting selection for migration efficiency comes at a cost to bulk growth rate.
13. **Q: Does the model include gas production?**
    - **A:** Currently just gravity and density. Reducing growth in the model slowed the wave, which contradicts the experimental data.
14. **Q: Is swimming costly?**
    - **A:** Yes. In aerobic flasks where oxygen is everywhere, the swimmers are quickly out-competed by non-swimmers.
15. **Q: Is the current still there when they swim?**
    - **A:** Likely, but we observe them slowing down in larger tubes where the convective current is most turbulent.
16. **Q: Do non-swimmers move at all in small tubes?**
    - **A:** In 2mm PVC, non-motile strains showed zero expansion, indicating the convective current was too weak to carry them.
17. **Q: Is selection happening at the wall?**
    - **A:** Possibly, but regaining motility is genetically difficult, so we haven't seen "re-swimmers" emerge yet.
18. **Q: Why do motile strains win so decisively in PVC?**
    - **A:** PVC is an oxygen bottleneck. Swimmers reach the oxygen front first.

---

## 5. Comprehensive Summary

**Motivation and Central Argument:**
The EVOGOLD project seeks to redefine laboratory evolution by selecting for **spatial migration** and **buoyancy control** in a flow-driven environment. The central argument is that evolutionary success in long towers depends on the ability to "surf" metabolic convection currents, which consistently leads to mutations in signaling hubs like **cyclic-di-AMP (GDPP)**.

**Key Conclusions:**

1. **Migration vs. Greed:** In the tower, being a "fast surfer" is more critical than being a "fast grower." Evolved strains often show reduced growth rates in flasks but superior migration in the tower.
2. **Genomic Convergence:** The recurrent targeting of gene 1816 across different conditions identifies it as a universal adaptive hub for buoyancy regulation in *Bacillus subtilis*.
3. **Motility Trade-offs:** While swimming provides a massive advantage for oxygen access in closed systems (PVC), it is energetically costly and can be hindered by the fluid "treadmill" effect in strong currents.

**Limitations and Future Work:**
The primary limitation is the oxygen bottleneck created by PVC tubing. Future experiments will focus on oxygen-permeable **silicon tubing** and the use of **CRISPR reversion** to validate the GDPP mutations. Additionally, direct **buoyancy assays** are needed to confirm the phenotypic link between osmotic signaling and cellular density.

***Note on Transcription Corrections:** The term "evil gold" has been corrected to **EVOGOLD**. "Cyclic IAMP/IAP" has been corrected to **cyclic-di-AMP**. "Bacillus cyclists" has been corrected to **Bacillus subtilis**.*
