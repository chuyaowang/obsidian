# Parametrizing Protein Allocation Models: How Evolution Shapes Enzyme Turnover Numbers to Support Cellular Objectives

**Speaker:** Samira van den Bogaard
**Affiliation:** RWTH Aachen University, Institute of Applied Microbiology
**Event:** AIMMS Symposium 2025
#seminar 

---

## Executive Summary

This talk addresses a practical bottleneck in metabolic engineering: protein allocation models (PAMs) — which extend genome-scale models with explicit enzyme constraints — require kcat (catalytic turnover number) parameters for every enzyme-reaction pair. For non-model microorganisms, these parameters are rarely available. Van den Bogaard presents an integrated computational framework that uses easily measurable extracellular exchange fluxes to infer and optimise kcat values, grounded in the biological insight that microorganisms have evolved enzyme kinetics in response to environmental pressures. The framework combines PAMs, a sensitivity analysis method (SENSE), and a genetic algorithm, and is validated against experimental growth data for *E. coli*.

---

## 1. Motivation: The Parameterisation Gap in Applied Microbiology

At RWTH Aachen's Institute of Applied Microbiology, the standard workflow for strain engineering is: collect experimental data → build computational models of increasing complexity → use models to predict strain designs → validate with new experiments. A particularly valuable model class is the protein allocation model (PAM), which captures how the finite protein budget of a cell constrains metabolic fluxes and growth.

Unlike genome-scale metabolic models (GEMs), which constrain only stoichiometry and flux directions, PAMs associate each reaction with an enzyme and its kcat value. This allows the model to predict how overexpressing a heterologous enzyme might reduce growth (by consuming protein budget) or how a production pathway competes with growth for protein resources. These predictions are critical for rational strain design.

**The problem:** kcat values must come from databases (BRENDA, the Bar-Even dataset) or from quantitative proteomics. For uncommon microorganisms — the ones most relevant to biotechnology — neither source is available in sufficient depth. The question therefore becomes: is there another way to estimate these parameters?

---

## 2. Biological Foundation: Environmental Constraints Shape Enzyme Kinetics

Microorganisms inhabiting fluctuating environments (such as *E. coli* in the gut) face two opposing selective pressures:

- **Substrate limitation**: when nutrients are scarce, growth rate is limited by the rate at which substrate can be acquired. Selection favors efficient substrate scavenging.
- **Protein limitation**: when nutrients are abundant, all substrate could in principle be metabolised, but there are not enough intracellular protein resources to do so. Selection favors high-kcat enzymes that deliver more catalytic power per unit protein mass. This regime is often associated with overflow metabolism and byproduct formation (e.g., acetate excretion in aerobic *E. coli*).

This dichotomy suggests a quantitative relationship: the extracellular exchange fluxes (how much substrate is taken up, what products are excreted, at what growth rate) encode information about the internal enzyme kinetics that have evolved to produce those phenotypes. **Can we use exchange fluxes to estimate kcat values?**

Two additional open questions motivate the work:
1. Is the relationship between exchange rates and kinetic parameters quantifiable, and if so, is it general enough to transfer across growth conditions?
2. Can we translate parameters estimated from one condition to predict behaviour in another?

---

## 3. Modelling Framework: Protein Allocation Models

### 3.1 Structure of a PAM

In a PAM, all metabolic reactions are associated with enzymes and their efficiencies. The total protein pool is partitioned among:

- **Enzymatic proteins**: each reaction i requires a minimum amount of enzyme proportional to its flux divided by kcat: $[E_i] ≥ flux_i / kcat_i$
- **Translational machinery**: ribosomes and translation factors whose abundance is linked to growth rate
- **Unused protein sector**: a reserve maintained for flexibility in changing environments

This unused protein sector is biologically important. It explains why in vitro kcat values (measured under saturating substrate) often do not match apparent in vivo kinetics — in most conditions, significant protein is held in reserve rather than actively catalysing reactions. This also means that the organism is not "optimal" in every condition, but is adaptable across conditions.

A PAM therefore ticks three boxes: it has the stoichiometric constraints of a GEM; it incorporates protein partitioning; and it assumes that not all proteins are fully utilised at all times.

---

## 4. Methodology: Three Integrated Tools

### 4.1 SENSE: Sensitivity Analysis for Identifying Critical kcats

Randomly optimising all kcat values simultaneously would be computationally intractable (thousands of parameters) and biologically uninformative. The authors developed **SENSE**, a sensitivity analysis that identifies which kcat values most strongly determine the model's predicted phenotype.

SENSE systematically perturbs individual kcat values and measures the resulting change in key outputs (growth rate, metabolite fluxes). Enzymes with high sensitivity are "rate-limiting" — small changes in their kcat propagate to large phenotypic changes. Enzymes with low sensitivity are either operating well below saturation or are not active under the condition analysed.

Focusing the genetic algorithm on sensitive enzymes reduces the optimisation problem from hundreds to tens of parameters, making it computationally feasible and biologically interpretable.

### 4.2 Genetic Algorithm: Running Evolution on a Computer

A **genetic algorithm** is a stochastic search method that mimics biological evolution. For this application:

- Each candidate solution is a vector of kcat values for the sensitive enzymes
- A population of candidate solutions is initialised
- In each generation: solutions are evaluated for how well the model predictions match experimental exchange flux data; high-fitness solutions are selected and reproduced; random mutations and recombination generate new candidates
- This iterates until convergence

Because genetic algorithms are stochastic and explore parameter space broadly, multiple independent runs produce different but equally valid kcat distributions. Crucially, this generates an **ensemble of models** rather than a single solution — important for exploring the feasible parameter space and for estimating prediction uncertainty.

### 4.3 Integrated Workflow

1. Start with a PAM using generic kcat values from BRENDA / Bar-Even (the baseline)
2. Run SENSE to identify the most sensitive enzymes
3. Apply the genetic algorithm to optimise those kcats against experimental exchange flux data (glucose uptake rate, oxygen uptake rate, acetate excretion, etc.)
4. Feed optimised kcats back into the PAM
5. Iterate; produce an ensemble of optimised models from multiple GA runs

---

## 5. Results: Validation Against *E. coli* Data

### 5.1 Fitting Experimental Data on Glucose

The optimised models were compared against measured exchange rates across a range of conditions for *E. coli* growing on glucose. The baseline model (generic kcats, analogous to a standard GEM) showed significant discrepancies. After several rounds of GA optimisation:

- Multiple independent GA runs converged toward similar regions of kcat space, indicating robust solutions
- Ensemble predictions matched experimental exchange flux data substantially better than the baseline
- The optimised models collectively captured the organism's phenotype much more accurately

### 5.2 Comparison With Literature kcat Values

The optimised kcat distributions were compared against BRENDA measurements and the Bar-Even dataset. Key finding:

- For **central carbon metabolism enzymes** (glycolysis, TCA cycle): optimised kcats were higher than baseline and aligned well with literature values. These enzymes must process high fluxes and have therefore evolved to be fast.
- For **peripheral enzymes** (amino acid biosynthesis, cofactor synthesis): optimised and baseline kcats clustered similarly, suggesting these enzymes are not rate-limiting for growth on glucose.

This pattern makes biological sense and provides external validation: evolution has optimised the enzymes where efficiency matters most (central carbon fluxes) while peripheral enzymes remain less constrained.

### 5.3 Transferability to Other Carbon Sources

Models optimised on glucose were tested (parameters fixed) against growth on alternative carbon sources. Predictions were better than the baseline GEM but not perfect — the optimised models predicted slower growth than observed ("more protein-burdensome"). This partial transferability reveals:

- Some aspects of kcat evolution are condition-general (central carbon kinetics transfer)
- Other aspects are condition-specific (different carbon sources impose different rate-limiting steps)
- Including growth on multiple carbon sources during parameterisation is a logical next step

---

## 6. Q&A

**Q: kcat values varied by several orders of magnitude. Is one high-kcat enzyme responsible for the main phenotype, or are multiple pathway enzymes collectively sensitive?**
The sensitive enzymes form a pathway rather than a single dominant enzyme. While individual kcat magnitudes differ, the relative ordering within a pathway is preserved across ensemble members. This is consistent with the principle of metabolic balance: natural selection distributes flux control among pathway steps rather than allowing one step to dominate. For engineering purposes, optimising whole pathways matters more than individual enzymes.

**Q: Should Vmax (= kcat × protein concentration) be optimised rather than kcat alone?**
An excellent point. In vivo, the relevant quantity is Vmax — the actual catalytic capacity determined by both turnover rate and enzyme abundance, which can vary by orders of magnitude across proteins. The framework focuses on kcat for pragmatic reasons: it is a property the cell's engineering machinery can alter (by changing enzyme identity or amino acid sequence), whereas protein abundance is more easily controlled by regulatory means. From a fundamental perspective, jointly optimising both is the more complete formulation and may be worth pursuing.

---

## 7. Comprehensive Summary

### Core Contribution

The framework demonstrates that extracellular exchange fluxes — easily measured quantities — do encode information about evolved intracellular enzyme kinetics. By using PAMs as the model structure, SENSE to identify important parameters, and genetic algorithms to optimise them, the approach enables kcat parameterisation without proteomics data. This opens protein allocation models to non-model microorganisms where such data are unavailable.

### Biological Insight

Evolution has tuned enzyme kinetics to match environmental demands. Central metabolic enzymes that handle high fluxes have high kcats; peripheral enzymes are less constrained. The evolved kcat distribution is not random — it reflects the cellular objectives (growth maximisation) and the environmental constraints (substrate and protein limitation) the organism has faced over evolutionary time. This makes it possible to reverse-engineer kinetic parameters from phenotypic data.

### Limitations

- Parameters optimised on one carbon source transfer only partially to others; condition-specific parameterisation or multi-condition optimisation is needed
- The model treats kcat as fixed; real enzymes are subject to allosteric regulation and post-translational modifications
- The unused protein sector fraction must be assumed or estimated, introducing uncertainty
- For organisms very distant from reference strains, BRENDA-derived initialisation may introduce systematic bias

### Future Directions

1. **Multi-condition parameterisation**: include growth data on multiple carbon sources simultaneously in the GA fitness function to improve transferability
2. **Non-model organisms**: apply the framework to industrially relevant strains (e.g., *Corynebacterium glutamicum*, *Bacillus subtilis*) where databases are sparse
3. **Vmax optimisation**: extend the framework to jointly optimise kcat and enzyme expression levels
4. **Experimental validation of strain designs**: use the parameterised models to propose specific gene deletions or overexpressions, then validate predictions in the laboratory

---

*Background notes: BRENDA (Braunschweig Enzyme Database) is a curated repository of enzyme kinetic parameters. Bar-Even et al. (2011) is a landmark analysis of enzyme kcat distributions across metabolic pathways. A genetic algorithm is a stochastic optimisation method inspired by Darwinian evolution (mutation, crossover, selection). SENSE is a model-internal sensitivity analysis method developed by the group.*
