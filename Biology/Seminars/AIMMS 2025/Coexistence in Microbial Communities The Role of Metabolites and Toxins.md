# Coexistence in Microbial Communities: The Role of Metabolites and Toxins

**Speaker:** Meike Wortel
**Affiliation:** University of Amsterdam
**Event:** AIMMS Symposium 2025
#seminar 

---

## Executive Summary

Meike Wortel addresses one of the central puzzles of microbial ecology: what maintains diversity in microbial communities? She argues that **frequency-dependent selection** is the primary driver, operating through two mechanisms — intraspecific competition (you compete more with your own type than with others) and niche creation (one organism generates an opportunity for another). Both require evolutionary trade-offs: without trade-offs, a single superior type would exclude all others. The talk is structured around two case studies. The first uses kinetic metabolic models to compute the feasible trade-off space between growth at low and high substrate concentrations, predicting coexistence of specialists under fluctuating environments. The second uses population-level modelling and experimental validation to predict coexistence between antibiotic-resistant and antibiotic-susceptible *E. coli* strains, mediated by beta-lactamase-driven cross-protection. A final, more speculative section explores interactions between metabolism and antibiotic resistance mechanisms.

---

## 1. Conceptual Framework: Frequency-Dependent Selection and Trade-offs

### 1.1 The Problem of Diversity Maintenance

Microbial communities are remarkably diverse, with hundreds to thousands of species coexisting in many environments. Competitive exclusion — the principle that a superior competitor should eventually displace all inferior ones — predicts much lower diversity than observed. The question is: what prevents this?

Wortel's answer: **frequency-dependent selection** — a situation where the fitness advantage of a type decreases as that type becomes more abundant. This creates a self-limiting dynamic that stabilises intermediate frequencies of multiple types.

Two distinct mechanisms generate frequency-dependent selection:

1. **Intraspecific competition dominates**: organisms of the same type compete with each other more strongly than with other types. This can arise from ecological specialisation — if two types use different substrates or occupy different niches, they limit each other less than they limit themselves. Coexistence is maintained because becoming more abundant means competing more with your own type.

2. **Niche creation**: one organism creates an ecological opportunity for another. Cross-feeding (consuming a metabolite that would otherwise inhibit or go unused) and detoxification (degrading a toxin that would suppress a susceptible partner) are examples. Again, the more abundant the detoxifier, the more toxin is degraded, which disproportionately benefits the susceptible type — a frequency-dependent effect.

### 1.2 The Requirement for Trade-offs

For frequency-dependent selection to maintain coexistence, trade-offs are necessary. Without them, a "Darwinian demon" — hypothetical organism optimal at all tasks — would outcompete everything. In reality, no organism is best at all things simultaneously: being a good competitor at low substrate concentrations (high transporter investment) means having fewer ribosomes available and growing slowly when substrate is abundant. These trade-offs are the mathematical precondition for coexistence.

Wortel organises the talk around two stories: one about **fluctuating environments maintaining coexistence** (mechanism 1) and one about **cross-protection leading to coexistence** (mechanism 2).

---

## 2. Story 1: Fluctuating Environments and Evolutionary Trade-offs

### 2.1 Historical Motivation: Coexistence of Two *E. coli* Strains in Serial Transfer

The first story is motivated by experimental results from the 1970s. Two strains of *E. coli* were propagated by serial transfer (a cyclically fluctuating environment: nutrients start high, decline to low by the end of each transfer cycle). Starting from very different initial frequencies, the two strains converged to stable intermediate frequencies — a classic signature of frequency-dependent selection.

The original researchers hypothesised this was due to specialisation on low vs. high nutrient concentrations within each cycle. Though it was later shown that the underlying mechanism was different, the conceptual model remains useful: one type with high substrate affinity (low Ks, low mumax — "low-substrate specialist") and another with high maximum growth rate (high mumax, high Ks — "high-substrate specialist") could stably coexist in a fluctuating environment. The key is that the more abundant a type, the shorter the period within each cycle at which it has a competitive advantage (because it depletes the substrate more quickly).

Wortel also connects this to the Lenski long-term evolution experiment, where coexistence of two *E. coli* types has been observed over thousands of generations of serial transfer.

### 2.2 Metabolic Models to Compute the Feasible Phenotype Space

The key contribution of Wortel's group is using metabolic models to compute what trade-off curves are actually achievable — i.e., which combinations of (mumax, Ks) pairs are physically feasible given the constraints of biochemistry and protein allocation.

The procedure:

1. Take a kinetic metabolic model (either a detailed *E. coli* central carbon metabolism model, or a more coarse-grained model with glycolysis, fermentation, and respiration modules)
2. Optimise the model at different substrate concentrations using **resource allocation** — deciding how much enzyme to invest in each pathway
3. For each optimised model (specialist at a given substrate concentration), fit the resulting growth curves to the **Monod equation** (µ = mumax × S / (Ks + S)) to extract population-level parameters
4. Plot all (mumax, Ks) pairs and draw the boundary — the feasible phenotype space

For the coarse-grained model, respiration and fermentation represent the two ends of the metabolic spectrum. Allocation decisions (how much enzyme is invested in each module) determine where along the trade-off curve an organism sits.

### 2.3 Predicting Coexistence

Using the computed trade-off curves, Wortel asked whether coexistence of *E. coli* and *Saccharomyces cerevisiae* under fluctuating conditions is predicted. The answer is yes: there is a region of parameter space where both organisms can coexist because intraspecific competition dominates, driven by their different positions along the growth trade-off curve.

**Limitations:** Experimental validation for this particular story is difficult (predicting which mutations invade a coexisting community and whether coexistence is evolutionarily stable is computationally demanding), which motivated the second, more experimentally tractable story.

---

## 3. Story 2: Cross-Protection and Antibiotic Resistance

### 3.1 Setup: TEM-1 Beta-Lactamase Degrades Ampicillin

The second story uses antibiotic resistance as a model system for niche creation. *E. coli* expressing TEM-1 beta-lactamase degrades beta-lactam antibiotics (specifically ampicillin and cefotaxime). In a mixed population of resistant (TEM-1-expressing) and susceptible (non-expressing) cells:

- When resistant cells are abundant, they rapidly degrade the antibiotic, lowering the environmental antibiotic concentration. Susceptible cells benefit — the environment becomes habitable for them.
- When resistant cells are rare, antibiotic degrades more slowly, maintaining high environmental concentrations. This is beneficial for resistant cells (which grow better in the presence of antibiotic relative to susceptibles).

This is again frequency-dependent selection: being more abundant reduces your relative fitness advantage. Additionally, there is a trade-off: the resistant strain grows slower than the susceptible strain at zero antibiotic concentration (resistance is costly).

### 3.2 Population-Level Model and Experimental Validation

Wortel's group wrote differential equations describing:
- Resistant cell density over time
- Susceptible cell density over time
- Antibiotic concentration over time

Parameters were measured experimentally in a collaboration with Wageningen: growth rates at various antibiotic concentrations (giving the trade-off), death rates, and antibiotic degradation rates.

**Predictions:** At low cell density and high antibiotic concentration: resistant type dominates. At high cell density and low antibiotic concentration: susceptible type dominates. A region in the middle allows coexistence of both.

**Experimental validation:** Experiments performed in Wageningen (by Philippe and Elina) confirmed coexistence in exactly the predicted parameter range, **without any parameter fitting** — the model predictions were made a priori from independent measurements. This is a strong validation.

Evolutionary follow-up analyses suggest coexistence is also maintained in evolutionary time (i.e., no mutation can easily invade and break coexistence), though this remains work in progress.

---

## 4. Story 3 (Outlook): Interactions Between Metabolism and Toxin Resistance

### 4.1 Toxic Metabolic Byproducts: Ethanol Self-Inhibition in Yeast

Using the coarse-grained yeast metabolic model, Wortel extended the model to include the fact that ethanol — a fermentation byproduct — inhibits fermentative growth. In an evolutionary simulation (chemostat with mutation and selection):

- Initially, fermentative phenotypes dominate (fast growth on abundant glucose)
- Ethanol accumulates and begins inhibiting fermentative cells
- Selection favours some respiratory cells, which are less inhibited
- In the end: stable coexistence of fermentative and respiratory cells

A notable result: **total community biomass at coexistence is lower than the initial single-type biomass**. Community-level biomass is not maximised; frequency-dependent selection produces a community that is stable but not optimal from a collective standpoint.

### 4.2 External Toxins: Antifungal Resistance in *Candida albicans*

In a more speculative extension, Wortel's group modelled antifungal resistance to fluconazole in *Candida albicans*. Fluconazole inhibits the ergosterol biosynthesis pathway (lipid membrane integrity). Possible resistance mechanisms include:

- Reduced import of the drug
- Increased efflux
- Target overexpression

Using the extended metabolic model, preliminary results showed:
- Under fermentative metabolism, export is the optimal resistance mechanism
- Under respiratory metabolism, import reduction is optimal
- At low glucose concentrations, target overexpression is optimal; at higher concentrations, export dominates

**Implication:** The metabolic mode (respiratory vs. fermentative) and nutrient availability in the community environment can determine which resistance mechanism evolves — and conversely, resistance mechanisms affect the external drug concentration and thereby influence other community members. This bidirectional coupling between community ecology, metabolism, and resistance evolution is a promising and largely unexplored research area.

---

## 5. Q&A

**Q: Protein synthesis costs energy — what is the difference between energy costs and protein costs for resistance mechanisms?**
Both energy and protein are ultimately derived from carbon flux. However, some resistance mechanisms (e.g., active efflux pumps) require ATP for transport, while others (e.g., target overexpression) primarily require protein. The relative cost depends on whether the limiting resource in a given condition is energy or protein. This distinction remains an open mechanistic question.

**Q: The trade-off curves shown have multiple phases and kinks rather than a simple monotone relationship. Does this reflect different constraints being hit at different points?**
The multiple-phase shape may partly be an artifact of the method: taking all possible flux distributions rather than only Pareto-optimal strategies. If only the evolutionary "best" strategies (Pareto front) were retained, some kinks might disappear. The biologically meaningful part of the trade-off is the region with high mumax values.

**Q: Can coexistence communities enable evolution of otherwise unreachable mutations?**
An open and interesting question. In principle, a community context could make previously neutral or inaccessible mutations beneficial by changing the environmental landscape (e.g., nutrient concentrations, toxin levels). This is unexplored territory.

---

## 6. Comprehensive Summary

### Central Argument

Coexistence in microbial communities is maintained primarily by frequency-dependent selection. This operates either through intraspecific competition (ecological specialisation in fluctuating environments) or niche creation (cross-protection, cross-feeding, detoxification). Both require evolutionary trade-offs. Wortel's group uses kinetic metabolic models — not genome-scale FBA — to compute the feasible phenotype space encoding these trade-offs, and population-level differential equations to make quantitative coexistence predictions. The antibiotic resistance case study provides experimental validation of the theoretical framework without parameter fitting.

### Role of Metabolic Models

A distinctive methodological contribution is using metabolic models to compute population-level parameters (mumax, Ks) rather than treating these as free parameters. This bridges intracellular biochemistry and community ecology: resource allocation decisions at the enzyme level translate into phenotypic trade-offs at the population level, which in turn determine community composition dynamics.

### Limitations

- The fluctuating-environment coexistence story lacks direct experimental validation; mathematical results assume idealised dynamics
- The interaction between metabolism and resistance mechanisms is at a very preliminary stage
- Community biomass not being maximised at coexistence is an interesting result but has not been experimentally verified
- Models are coarse-grained; predictions at the molecular mechanistic level require more detail

### Future Directions

1. **Experimental validation of trade-off curves**: measure mumax and Ks of natural and engineered *E. coli* variants and compare to predicted feasible phenotype space
2. **Evolutionary stability analysis**: test whether predicted coexistence equilibria are resistant to invasion by novel mutants
3. **Fluconazole resistance in Candida**: extend the metabolic model and validate resistance mechanism predictions experimentally
4. **Community-level effects on resistance evolution**: design experiments to test whether community composition influences which resistance mechanisms arise
5. **Combining stories**: integrate the fluctuating-environment and cross-protection frameworks into a single unified model of diversity maintenance

---

*Background: Darwinian demons = hypothetical organisms with no evolutionary trade-offs, i.e., optimal at everything. Monod kinetics describe growth rate as µ = mumax × S/(Ks + S) where S is substrate concentration, mumax is maximum growth rate, and Ks is the half-saturation constant. TEM-1 is a class A beta-lactamase conferring resistance to ampicillin and related penicillins. The Lenski long-term evolution experiment has propagated E. coli by serial transfer since 1988, the longest running evolution experiment with a microorganism.*
