# 13C MFA Study

> [reference](file:///Users/wangchuyao/Documents/seminars/mfa/model/High-Res%2013C%20MFA.pdf)
## 1. Model assumptions

- *Metabolic steady state*: fluxes do not change
- *Isotopic steady state*: isotopic labeling does not change. Other flux analyses for non steady state exist such as 13C-NMFA and 13C-DMFA
- *No kinetic isotope effect*: labeling does not change enzyme kinetics
- *No metabolite channeling*: metabolite does not go from one enzyme directly to another
- *Pure isotopic tracers*: tracers are chemically pure, and have high isotopic purity at the specified carbon positions
- *Homogeneous metabolite pools*: the intracellular environment is perfectly mixed
- *Phenotypically homogeneous culture*: all cells have the same phenotype. Other analyses exist for coculture of two microbes. A **G** parameter can be introduced when the culture contain unlabeled biomass before the beginning of experiment. For example, this can come from the inoculum.
- *No turnover of macromolecules*: macromolecules are not produced and broken down at the same time. Turnover can be modeled by additional fluxes if assumed to exist.
- *Adequate metabolic model*: the model captures all relevant reactions, and reaction stoichiometries and atom transitions are correct. Models may be not correct when there are unknown enzymes, undocumented reactions, reactions caused by promiscuous enzymes, and reactions with alternative atom transitions. Sometimes the model must be adjusted to achieve an acceptable fit, and follow-up experiments are needed to verify the model adjustments.

## 2. Experiment Workflow

### [Tracer](tracers) selection

- Determined via in-silico simulation + experimental confirmation; Different for single, double, and multi labeled experiments. Review available. For high resolution flux determination, parallel labeling with 2 or 3 tracers yields better results.

### Metabolic Steady state

- Continuous culture: running the culture for at least 5 residence times.
- Batch culture: sample the culture during early to mid of the exponential growth phase, as metabolic shifts happen when glucose is depleted or byproducts such as acetate accumulates to a high level.
- At metabolic steady state the curve should vary linearly with time.
- Determine at metabolic steady state: growth rate, biomass yield on glucose, acetate produced per amount of biomass, acetate yield on glucose.

### External Rates

- Measured during **batch culture**, not pre-culture.
- Isotopic labeling data provide information on relative pathway usage.
- At least **one** external rate (substrate uptake) is required to get absolute flux values.
- Growth rate determination: plotting the ln of biomass concentration vs. time and quantify the slope.
- Biomass yield: biomass concentration vs. glucose concentration and quantify the slope.
- OD600 to biomass conversion factor: converts OD600 value to grams of dry weight per liter.
- Product yield: product concentration vs. glucose concentration and quantify the slope.
- Amount of product per biomass produced: product concentration vs. biomass concentration and quantify the slope.
- External rates should only be computed during metabolic steady state (i.e. early to mid exponential growth or OD600 < 1).
- Glucose uptake rate and product secretion rate can be computed after the rates above are calculated (see model for equation).

### Metabolic Model

- The minimum scope of the model should explain the possible origins of all measured metabolite atoms.
- For proteinogenic amino acids, the model must include substrate uptake, central carbon metabolism, and amino acid biosynthesis pathways.
- A biomass synthesis equation should be determined for non-model organism (see paper for method). 
> [!info] From Antoniewicz himself's email
> 
Update: the biomass equation does not have a large impact on the result.
- The model should account for incorporation of atmospheric CO2, which can dilute isotopic labeling.
- In some cases turnover of macromolecules needs to be accounted for.

### MFA Simulation

- [INCA](INCA.md), Metran
- Fluxes are computed by minimizing error between measured and simulated measurements using non-linear least squares regression.
- The iterative fitting process is repeated many times with different random starting points until a single convergent solution is reached.

### Statistical Analysis

- Verify **goodness of fit** and **confidence interval**.
- If the model is adequate and the measurements are without gross errors, the *variance weighted SSR* (sum of squared error) should be a stochastic variable with a chi-square distribution, with dof equal to the number of fitted measurements (MDVs) n minus the number of fitted parameters (fluxes) p. An acceptable range for SSR is computed from the chi-square distribution given a chosen threshold, for example 0.05 for 95% confidence intervals.
- The *weighted residuals* should be normally distributed, and outliers should be evaluated.
- Confidence interval for each flux value is computed with parameter continuation or Monte Carlo simulations.
	- Parameter continuation: vary each parameter and compute SSR deviation.
	- Monte Carlo: generate synthetic datasets using the flux values, add noise, and refit flux values.

> [!note] More about SSR
> 
> SSR的大小是相对的，它是根据拟合过程中预测的同位素分布向量和实际的mdv间的差距计算出来的，比如一个C3的化合物，预测的是[0.5,0.4,0.1]，实际的是[0.6,0.3,0.1]，就会根据这个分布算一个误差值出来，把所有mdv的误差加起来就是SSR，所以化合物越多SSR越高。
> 理论上SSR呈卡方分布，被（mdv的数目 - 反应式的数目）的值定义，可以用这个分布计算出一个95% confidence的上下限，如果在迭代优化最后SSR在这个范围里面就判断结果可信度较高
### Evaluating Results

- If the SSR is out of range or any of the simulated isotope labeling have very high residuals, the result is not correct. Possible source of error is the network model. The model can be modified based on re-examining the model assumptions, consulting the literature, and novel hypothesis. *Note* that if the fluxes with high residuals are clustered together, reactions may be missing there.
- If the SSR is ok, the next step is to check whether the flux values are resolved. The resolution is evaluated by looking at the confidence intervals of the fluxes.

## 3.  Materials

### Reagents

- [Tracers](tracers.md): \[1,2-13C] glucose and \[1,6-13C] glucose. The chemical purity and isotopic purity should be > 99%. The purity should be verified.
- Naturally labeled glucose (Sigma Aldrich, cat. no. G7021).
- Minimal medium: contains nutrients just enough for survival (M9 minimal medium; Sigma Aldrich, cat. no. M6030).
- Rich medium: contains more nutrients (LB medium; Sigma Aldrich, cat. no. L3152)
- Both these mediums are liquids.
- Microbial strain (frozen stock or colonies on agar plate).

### Reagents Setup

#### Glucose stock solutions

- Prepare stock solutions of unlabeled and 13C tracer glucose in 20% wt/vol in DI water.

#### Unlabeled growth medium for pre-culture

- Prepare minimal or rich medium with naturally labeled glucose. Sterilize by filtration.

#### 13C-labeled media

- Use minimal M9 medium with 2g/L glucose tracers.

## 4. Procedure

### Pre-culture cells in unlabeled medium; 12-18h

1. Inoculate a pre-culture using [unlabeled medium](####Unlabeled%20growth%20medium%for%pre-culture) (10 to 25 mL liquid volume) with cells from frozen stock or a colony from an agar plate.
   **Note**: for slow growing strains, use rich medium.
2. Grow the cells overnight at the desired temperature, aeration, and mixing conditions.
3. Wash the cells once with fresh medium without any carbon source by first centrifuging the cell culture (14,000 g for 5 min at 2 °C), removing and discarding the supernatant, and resuspending the cell pellet in an equal volume of fresh medium that does not contain any carbon sources.
   **Note**: the cells must be washed to avoid carrying carbon sources to the labeling experiment.

### Parallel labeling experiment with 13C tracers

> Use batch culture to investigate metabolism at maximum growth rate.

1. Inoculate cells from the pre-culture into the tracer media (10 mL volume) at a low cell density (OD600 ~ 0.01). The exact fraction of unlabeled biomass is estimated by the G parameter in 13C-MFA. High initial densities may be used, but DNA, RNA, and protein turnover will introduce non-negligible flux of unlabeled metabolites that should be accounted for in the analysis.
2. Grow the cultures at constant growth rate. If the bacteria produce acid, pH should be maintained constant by adding buffers.
3. Sample hourly or every 30 minutes and measure OD600 values. The sampling volume can be kept low by using microcuvettes to take OD600 measurements. Centrifuge the samples at 14,000 g for 5 min at 20 °C, and retain the supernatant for subsequent analysis of glucose and secreted products. Store the supernatants in a freezer.
4. When the cells reach mid-exponential phase (OD600 ~ 0.7), collect 6 1-mL samples from the cultures. Analyze 2, and store the rest for redundancy.
5. Immediately centrifuge the samples at 14,000 g for 5 min at 20 °C. Remove and retain 1 mL of supernatant for subsequent analysis.
6. Store the cell pellets and supernatant samples in a freezer.

### Analyze supernatant samples and calculate extracellular rates

1. Measure metabolite concentrations in the *supernatant* samples.
2. Calculate external rates and yields.

### Analyze metabolite labeling

1. Should be analyzed from the *cell pellets*.
2. Determine the isotopic purity of 13C-glucose tracers.