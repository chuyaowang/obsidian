# Alkaline pH-Driven Metabolic Plasticity of *Lactococcus lactis* FM03

**Speaker:** Tamara Bendig
**Affiliation:** Wageningen University
**Event:** AIMMS Symposium 2025
#seminar 

---

## Executive Summary

This talk presents a detailed physiological investigation of how *Lactococcus lactis* — the primary starter culture for cheese production — responds to alkaline pH (pH 8), an environment it rarely encounters naturally but may be intentionally exploited to improve starter culture functionality. Using a chemostat system with galactose as the carbon source and quantitative proteomics, the speaker characterises a multi-layer alkaline stress response: a metabolic shift from mixed-acid to homo-lactic fermentation driven by restricted enzyme capacity in the mixed-acid branch; thickening of the cell wall (confirmed by atomic force microscopy); and upregulation of peptide uptake, hydrolysis, and transamination pathways. Critically, these adaptations appear to leave a **metabolic memory** — cells habituated to alkaline pH continue to produce different flavour compounds (notably elevated benzaldehyde) even when returned to neutral conditions, with implications for cheese ripening and flavour development.

---

## 1. Introduction: Lactic Acid Bacteria and Alkaline Environments

### 1.1 Why Study Alkaline pH in *Lactococcus lactis*?

Lactic acid bacteria (LAB) are almost universally associated with acidic environments — they grow by fermenting sugars to lactic acid, lowering the pH of milk, vegetable brines, and other substrates. *Lactococcus lactis* is the workhorse of dairy fermentation, responsible for the initial acidification of cheese vats and contributing proteolytic enzymes central to flavour development during ripening.

Alkaline pH (above pH 7) is therefore typically considered outside the organism's relevant experience. Rare exceptions include:
- Accidental contamination of alkaline industrial cultures
- Presence in insect hindguts, where pH can reach 8.5–9 (e.g., wood-boring beetles, mole crickets)
- Nasal and oral environments

### 1.2 Why Alkaline pH Might Matter for Dairy Technology

Despite the unusual context, alkaline stress responses are interesting for two reasons. First, stress responses in general activate chaperone proteins (which refold misfolded proteins) and proteolytic enzymes — and **cheese ripening is fundamentally a proteolytic process**. The degradation of caseins by LAB proteases and peptidases, followed by further hydrolysis and transamination of released amino acids, generates the flavour compounds of aged cheeses. If alkaline stress activates these same systems, it may boost the proteolytic capacity of starter cultures.

Second, **cross-resistance** — the phenomenon where stress in one condition imparts protection or altered physiology in another — is well documented. Alkaline-habituated cells might be more robust starter cultures or produce different flavour profiles even after returning to normal cheese-ripening conditions.

The central research question of the PhD project: **can alkaline pH be exploited to improve the functionality of starter cultures?**

---

## 2. Experimental System

*L. lactis* FM03 was grown in a **chemostat** — a continuous culture system that maintains cells at a defined, constant growth rate (dilution rate, D) under nutrient limitation. Key experimental features:

- **Carbon source: galactose** (not glucose — this is explicitly noted by the speaker as important)
- Two experimental modes:
  1. **Variable dilution rate** at fixed pH — to study the effect of growth rate at pH 6 and pH 8
  2. **Variable pH** at fixed dilution rate (D = 0.2 h⁻¹) — to isolate the effect of pH

This chemostat design ensures that observed differences are due to pH (or growth rate) rather than transient effects, nutrient depletion, or growth phase.

---

## 3. Metabolic Shift: From Mixed-Acid to Homo-Lactic Fermentation

### 3.1 The Fermentation Modes of *Lactococcus lactis*

*L. lactis* can operate in two fermentation modes:

- **Mixed-acid fermentation**: produces lactate, formate, acetate, and ethanol. Typically occurs at low growth rates. More energy-efficient.
- **Homo-lactic fermentation**: produces only lactate (via lactate dehydrogenase, LDH). Typically occurs at high growth rates. Produces 2 ATP per glucose (or equivalent), and is thermodynamically simpler.

The switch between modes is well-characterised for glucose. The speaker observes it here for galactose under alkaline conditions.

### 3.2 Observed Shifts at Alkaline pH

Measuring metabolite production rates at pH 6 vs. pH 8:
- At pH 8, the metabolic mode shifts toward homo-lactic fermentation at lower dilution rates than at pH 6
- The shift is more pronounced and occurs earlier as growth rate increases
- The capacity of the mixed-acid branch (formate, acetate, ethanol production) is reduced at pH 8 and decreases further at higher growth rates (contrary to the stable pattern at pH 6)
- As a result of restricted flux through the mixed-acid branch, all available flux is forced through LDH

There is also a modest **energetic cost** at pH 8: slightly lower biomass yield, consistent with energy expenditure to maintain intracellular pH against the alkaline gradient.

### 3.3 Proteomics Reveals the Mechanism

To understand why the mixed-acid branch is restricted, the speaker performed quantitative proteomics at D = 0.2 h⁻¹, comparing pH 6 and pH 8 (log2 fold changes):

- **Glycolysis proteins**: neatly downregulated at pH 8
- **LDH (lactate dehydrogenase)**: approximately unchanged (slightly downregulated)
- **Yet**: the measured flux through glycolysis and LDH **increases 2.6-fold** at pH 8

This apparent paradox — lower enzyme levels but higher flux — indicates that the enzymes are working at **higher capacity utilisation** at pH 8. The restriction of the mixed-acid branch forces more flux through the LDH path, increasing LDH saturation and apparent flux even without more LDH protein.

**Mixed-acid branch enzymes** (pyruvate formate lyase B, PFLB; acetate kinase; alcohol dehydrogenase) are downregulated at pH 8 at the protein level. This directly explains the reduced flux through that branch — not a kinetic or thermodynamic constraint, but a reduction in enzyme abundance.

A linear relationship between PFLB protein abundance and formate flux was observed, confirming that protein level is the direct limiting factor in this branch.

---

## 4. Cell Wall Modulation

### 4.1 Proteomics Signature of Peptidoglycan Biosynthesis

Analysis of significantly changed proteins across pH conditions revealed a strong signal in cell wall biosynthesis:

- **Mur cluster proteins** (enzymes for peptidoglycan (PG) precursor synthesis): upregulated at pH 8
- **Penicillin-binding proteins** (PBPs, responsible for cross-linking PG strands): increased
- **D-alanine endopeptidase** (trims the pentapeptide stem, preventing cross-linking): upregulated (note: this may represent a recycling/remodelling function)
- **PG recycling enzymes**: upregulated — suggesting active turnover coupled to net synthesis
- **D-alanyl transferases** (add alanine to teichoic acids, making the cell wall surface more positively charged): upregulated — this would reduce leakage of positively charged protons through the cell wall

Together, this proteomic signature predicts a thicker, more extensively cross-linked, and more positively charged cell wall at alkaline pH.

### 4.2 Physical Confirmation: Atomic Force Microscopy

To confirm that the proteomic predictions translate to actual structural changes, the speaker used **atomic force microscopy (AFM)** to directly measure cell wall thickness.

**Result: the cell wall doubles in thickness at pH 8 compared to pH 6.**

This is a striking confirmation. Making the cell wall thicker at alkaline pH is interpreted as a strategy to reduce leakage of protons out of the cell (the alkaline environment "pulls" protons out, dissipating the membrane potential and reducing intracellular pH). A thicker wall provides an additional diffusion barrier.

Interestingly, the same response was discussed in the context of acidic pH: at low pH, a thicker cell wall would block proton entry into the cell. The cell wall thickening may therefore be a general stress protection strategy, regardless of direction.

---

## 5. Peptide Catabolism and Amino Acid Metabolism

### 5.1 Proteomic Changes in Peptide Metabolism

At pH 8, the following changes were detected:
- Many **peptide transporters** increased
- Many **amino acid transporters** increased (not shown in heat map, but noted)
- **Peptidases** (enzymes that hydrolyse peptides to free amino acids) increased — including PEP-N and PEP-X, which are known to reduce cheese bitterness
- **Aminotransferases** (enzymes that convert amino acids to α-keto acids, generating flavour-active compounds) increased

### 5.2 Industrial Relevance: Cheese Flavour Development

Cheese flavour arises from a complex cascade: proteolysis of caseins → release of peptides → hydrolysis to free amino acids → catabolism of amino acids to flavour-active volatiles (keto acids, aldehydes, alcohols, sulphur compounds). The speaker notes that:

- Increased peptide uptake + hydrolysis + transamination at alkaline pH represents upregulation of **key flavour development enzymes**
- The increase in **free amino acid production rates** was confirmed by measuring secretion rates of various amino acids at different pH levels

This suggests a mechanistic link: alkaline pH upregulates the proteolytic and catabolic machinery that cheese relies upon for flavour formation.

---

## 6. Metabolic Memory: Does the Alkaline Experience Persist?

### 6.1 Concept and Experimental Design

Since cells in a cheese vat undergo minimal cell division during ripening, any metabolic reprogramming acquired during the production phase (when the starter culture is grown at defined conditions) might persist as a **metabolic memory** or imprint that shapes flavour development over weeks.

To test this, the speaker distinguished two cell types:

- **Exposed**: grown at pH 6 in batch fermentation, then exposed to pH 8 for 2 hours before the experiment
- **Habituated**: grown for many generations in a chemostat at pH 8 (or pH 6 as control)

Both types were then resuspended in a **flavour formation buffer at pH 6** — simulating the cheese ripening environment — and the production of volatile flavour compounds was measured.

### 6.2 Key Result: Benzaldehyde as a Reporter

Benzaldehyde is an important aromatic flavour compound in cheese, derived from phenylalanine via transamination or direct decarboxylation. In the chemostat at pH 8 (pH-controlled):

- Benzaldehyde production is **3-fold higher** at pH 8 than pH 6
- The conversion of benzaldehyde to benzyl alcohol (a reduction reaction) appears **blocked** at pH 8
- The conversion of phenylalanine to phenylacetaldehyde via a second pathway appears blocked at alkaline pH (possibly because it involves a proton-dependent decarboxylation reaction)

In the flavour formation experiment (all cells now at pH 6 in buffer):

- **Habituated cells** (grown for many generations at pH 8) still produce **3-fold more benzaldehyde** than pH 6 controls — the elevated flux persists
- **Exposed cells** (brief pH 8 contact) produce similar benzaldehyde levels to the pH 6 control — no memory from brief exposure
- The block on benzaldehyde-to-benzyl-alcohol conversion persists in habituated cells
- Phenylacetaldehyde production is **restored** in the buffer at pH 6 (the decarboxylation is pH-dependent and recovers when pH is normalised)

**Conclusion**: metabolic memory exists for habituated cells but not for briefly exposed cells. The elevated benzaldehyde production in habituated cells reflects stable reprogramming of the aminotransferase pathway, rather than acute pH effects.

---

## 7. Q&A

**Q: If you really want to implement this in cheese production, is it practically feasible? Is there a concern about multiple generations between alkaline conditioning and ripening? And what other volatiles were changed?**
In milk, the high starter culture inoculation density causes very rapid acidification, so there is little time for cells to experience alkaline pH before the medium acidifies. A more feasible approach would be to use alkaline-habituated cells as an **adjunct culture** (added after primary fermentation rather than as the primary acidifier). A mini-cheese experiment showed that lipid-derived metabolites also changed, but the magnitude of change was much smaller than for benzaldehyde, which stood out clearly. Confirmation in a real product setting is still needed.

**Q: Is the cell wall thickening specific to alkaline pH, or does it also occur at acidic pH?**
Cell wall thickness was also measured at pH 7, where an intermediate thickness (~33 nm) was found. The speaker speculates this is a general strategy: a thicker cell wall is protective against proton flux in either direction — blocking proton entry at low pH and blocking proton efflux at high pH. A colleague noted that the same cell wall proteins show stress responses at low pH as well.

**Q: CO₂ solubility differs substantially between pH 6 and pH 8. Could this affect flavour compound production, since several mixed-acid fermentation reactions involve CO₂?**
Very interesting and previously unconsidered. CO₂ solubility is ~50-fold higher at pH 8 than pH 6 (as HCO₃⁻ is the dominant form at alkaline pH). This could affect reactions that produce or consume CO₂, including some mixed-acid branch enzymes and potentially some decarboxylation reactions in amino acid catabolism. Off-gas analysis was not performed in this study, so this remains an open question.

---

## 8. Comprehensive Summary

### Central Findings

1. **Metabolic shift**: *L. lactis* at alkaline pH shifts toward homo-lactic fermentation, driven by downregulation of mixed-acid branch enzymes at the protein level. Flux through LDH increases 2.6-fold despite lower glycolysis protein levels, indicating higher capacity utilisation.

2. **Cell wall remodelling**: Extensive upregulation of peptidoglycan synthesis, cross-linking, and teichoic acid modification enzymes leads to a doubling of cell wall thickness (confirmed by AFM). This physically protects against proton leakage in either direction.

3. **Peptide and amino acid catabolism**: Key peptide transporters, peptidases (PEP-N, PEP-X), and aminotransferases are upregulated, elevating amino acid release and conversion to flavour-active volatiles — the same biochemical processes central to cheese ripening and flavour development.

4. **Metabolic memory**: Habituated (not merely exposed) cells produce 3-fold more benzaldehyde than controls even when returned to normal pH, demonstrating that alkaline conditioning leaves a functional metabolic imprint.

### Implications

The findings suggest that alkaline pH conditioning could be used biotechnologically to improve starter culture performance: pre-treating *L. lactis* at alkaline pH before adding it as an adjunct culture could increase proteolytic and flavour-generating activity during cheese ripening, enhancing flavour quality without genetic modification.

### Limitations

- Results are from a defined experimental system (chemostat, galactose, one strain); behaviour in real milk and with commercial strains needs validation
- Metabolic memory was demonstrated only for one pathway (phenylalanine-to-benzaldehyde); its extent and specificity are unknown
- The mechanism maintaining the memory is not elucidated (epigenetic? protein pool composition? regulatory state?)
- CO₂ effects and off-gas contributions were not measured

### Future Directions

1. Validate metabolic memory in milk and cheese matrices
2. Explore other volatile flavour compounds beyond benzaldehyde
3. Investigate the molecular mechanism of metabolic memory (proteome persistence? regulatory protein states?)
4. Test whether the response is general across *L. lactis* strains or strain-specific
5. Design a practical adjunct culture protocol and validate in pilot-scale cheese production

---

*Transcript corrections: numerous transcription errors were present. "Naxxopolis" = Lactococcus; "salvo" = cell wall; "mole cheeks" = mole crickets; "cages" = pH; "gut cage of knife" = gut pH of 9; "Merck cluster" = Mur cluster (peptidoglycan synthesis enzymes); "trichuric acids" = teichoic acids; "benzaldehyde to benzaldehyde" = benzaldehyde to benzyl alcohol; "phenylpheromides of benzene acetaldehyde" = phenylacetaldehyde.*
