# Physiological stress drives the emergence of a _Salmonella_ subpopulation through ribosomal RNA regulation

#paper
[link](https://www.sciencedirect.com/science/article/pii/S0960982223013131?via%3Dihub)

## Abstract and Introduction

### Motivation and Core Questions

The primary motivation of this study is to understand how bacterial populations balance the massive degradation of ribosomes during starvation with the need to maintain evolutionary fitness and rapid growth potential when nutrients return. In nature, and specifically within the host gut or inside macrophages, enteric bacteria like _Salmonella enterica_ serovar Typhimurium (S.Tm) experience frequent "feast and famine" cycles.

The central question the study answers is: How do bacterial cells regulate the dynamics of massive ribosomal RNA (rRNA) degradation during starvation while ensuring population growth in changing environments?

### Biological Background and Key Concepts

For bioinformaticians, understanding the biological substrate is vital for modeling the data correctly. The study relies on several foundational biological concepts:

- rRNA (Ribosomal RNA): The non-coding RNA that serves as the primary structural and catalytic component of ribosomes, the cellular machines that synthesize proteins. Because ribosomes constitute a massive fraction of cellular mass, their regulation is heavily tied to cell growth rates.
- Stringent Response: A highly conserved bacterial stress response triggered by nutrient limitation. It is mediated by the alarmone molecule (p)ppGpp, which accumulates to repress the transcription of rRNA and induce survival mechanisms.
- Growth Phases: Bacteria in batch culture experience a "lag phase" (adapting to new nutrients), an "exponential phase" (rapid, continuous division), a "transition phase" (nutrient depletion slows growth), and a "stationary phase" (growth halts).
- Nutritional Upshift: The sudden restoration of nutrients to a starved population, forcing them to exit stationary phase and resume growth.
- Phenotypic Bimodality: The coexistence of two distinct phenotypic states within a genetically identical population.

### Methodological Innovation and Suitability

Historically, bacterial starvation responses were measured using bulk RNA sequencing or bulk protein assays. Bulk measurements indicated a homogenous 90% decrease in S.Tm rRNA levels during starvation.

The innovation of this study is the application of single-molecule fluorescence in situ hybridization (smFISH) targeting rRNA (rRNA-FISH) combined with flow cytometry and microscopy to measure single-cell rRNA dynamics. This method avoids the artifacts of genetically engineered fluorescent reporters (which can alter protein half-lives) by directly hybridizing to endogenous RNA transcripts.

This methodology is highly suitable for identifying and mapping cell-to-cell heterogeneity, stochastic gene expression, and subpopulation emergence in isogenic cultures—problems where bulk transcriptomics systematically fail by averaging out critical single-cell variances.

## Results

### Emergence of Ribosomal Bimodality

During the transition from exponential to stationary phase, the authors tracked 16S rRNA levels. Rather than a uniform decrease across all cells, the rRNA-FISH signal revealed a bimodal distribution. A large subpopulation degraded its rRNA heavily (16Slow), while a minor subpopulation maintained high ribosomal levels (16Shigh). The 16Shigh cells contained approximately 14-fold more 16S rRNA than the 16Slow cells.

The authors validated these imaging findings robustly. They used flow cytometry sorting coupled with RT-qPCR to confirm the transcript levels. Furthermore, they utilized liquid chromatography-tandem mass spectrometry (LC-MS/MS) on sucrose cushion-purified ribosomes to confirm that the rRNA-FISH signal corresponded to physically intact 30S and 50S ribosomal subunits. To ensure the low signal wasn't due to dead cells, they confirmed cellular viability using single-cell colony-forming unit (scCFU) assays and propidium iodide staining.

### Mathematical Modeling of Ribosome Dynamics

To determine the physical mechanisms driving this bimodality, the authors tested alternative theoretical hypotheses. They built ordinary differential equation (ODE) models to simulate two alternate paths: a purely dilution-based process versus an active degradation-based process.

#### Assumptions and Premises

The core premise is that cells in exponential growth maintain a steady-state ribosome concentration $r_0$. Upon detecting starvation, cells undergo a stochastic switch to turn off rRNA transcription. The time a cell takes to switch, $\Delta t$, is modeled as an exponentially distributed random variable based on a switching rate $\gamma_{rib}$: $p(\Delta t) = \gamma_{rib} e^{-\gamma_{rib}\Delta t}$

#### Algorithm and Model Description

1. Dilution Model: Assumes transcription stops at the switch time $t_{c}^{rib}$, and existing ribosomes are simply diluted as cells continue to divide. The volume grows, halving the concentration per division.

2. Active Degradation Model: In addition to transcription shutdown, an active mechanism begins degrading engaged ribosomes at a rate $\lambda_a$. Active ribosomes degrade, while inactive ribosomes $R_{in}$ are protected.

The deterministic rate of change for the number of ribosomes $R$ post-switch is given mathematically as:

$\frac{dR}{dt} = -\lambda_a (R(t) - R_{in}^f)$

By fitting these models to the quantitative FISH data, the authors found that a strictly non-zero active degradation rate was required to explain the dramatic 95% reduction in ribosomes, ruling out the alternate path of simple dilution.

### Phenotypic Fitness During Nutritional Upshifts

The authors sought to link this physical bimodality to an evolutionary or functional phenotype. Using distinct starvation media (carbon vs. phosphate limitation), they manipulated the proportion of the 16Shigh subpopulation. Carbon limitation preserved a higher fraction of 16Shigh cells compared to phosphate limitation.

When these starved populations were reintroduced to rich media (nutritional upshift), the carbon-limited cells (enriched for 16Shigh) resumed growth significantly faster, exhibiting shorter lag times. Using single-cell sorting, they proved that individual cells with shorter lag times corresponded proportionately to the cells bearing high ribosomal levels.

### Molecular Drivers: DksA and RNase I

To discover the genetic architecture behind this phenomenon, the authors executed a [Genome-wide Transposon Insertion Sequencing](Biology/Concepts/Genome-wide%20Transposon%20Insertion%20Sequencing.md) (TIS) screen. This is an unbiased method where random mutants are sorted by phenotype (16Shigh vs. 16Slow) and their disrupted genes are mapped via next-generation sequencing.

They identified two primary molecular drivers:

1. dksA: Encodes DksA, a transcription factor that acts synergistically with the stringent response to shut down rRNA transcription.

2. rna: Encodes RNase I, an endonuclease responsible for the active degradation of the rRNA.

Alternate paths were explored: the authors also checked hibernation factors (rmf, hpf, yfiA) and other RNases, but knocking these out did not abolish the bimodality, confirming the specific necessity of DksA and RNase I.

### Quantitative Results Summary

The data acquisition relied heavily on high-throughput single-cell imaging and flow cytometry, capturing fluorescent intensity as a proxy for RNA copy number, which was then computationally segmented and quantified.

|**Phenotype/Metric**|**16Shigh Subpopulation**|**16Slow Subpopulation**|**Source Reference**|
|---|---|---|---|
|**Relative 16S rRNA levels**|~14 to 19-fold higher|Baseline||
|**Transcription status**|Active|Repressed (DksA-mediated)||
|**Active Degradation**|Minimal|High (RNase I-mediated)||
|**Lag Time (Recovery)**|Short, rapid adaptation|Long, delayed recovery||

### Key Figures and Tables

- **Figure 1: Characterization of Ribosomal Bimodality in Single Cells**
  - **What it shows:** This is the foundational figure that characterizes the core phenomenon. It presents bulk growth curves (Panel A) matched with single-cell density histograms of 16S rRNA-FISH fluorescence (Panels B and D) and corresponding epifluorescence microscopy images (Panels C and E) across different growth phases. Panels G and H provide RT-qPCR and mass spectrometry validation of the FISH signals.
  - **Key Takeaways:**
    - **The Bimodal Split:** As the bacterial population exits exponential growth and enters the transition phase, it does not uniformly reduce its ribosomes. Instead, the data reveals a stark split into two distinct subpopulations: $16S^{high}$ and $16S^{low}$.
    - **Visual and Quantitative Proof:** The microscopy images directly validate the cytometry data, visually confirming that some individual cells maintain bright rRNA signals while neighboring cells dim significantly.
    - **Physical Ribosome Degradation:** The mass spectrometry data (Panel H) proves that the drop in FISH signal is not an artifact of probe accessibility; the actual, physically intact 30S and 50S ribosomal subunits are degraded by up to 95% as the population moves into late transition.
- **Figure 2: Evolutionary Conservation and Intracellular (In Vivo) Relevance**
  - **What it shows:** This figure answers whether ribosomal bimodality is a quirk of a single laboratory strain or a broader, biologically conserved strategy. Panels A and B use flow cytometry and microscopy to compare 16S rRNA levels across multiple _Salmonella_ strains (14028S, D23580, S4/74), _E. coli_, and _S. aureus_. Panels C and D shift to an _in vivo_ model, tracking S.Tm infecting J77A-1 macrophages over a 24-hour period.
  - **Key Takeaways:** 
    - **Conservation:** The bimodal split into 16Shigh and 16Slow subpopulations is deeply conserved across different S.Tm strains. However, it is _not_ observed in _E. coli_ or the Gram-positive _S. aureus_, which instead exhibit a more uniform, homogeneous decrease in ribosomes during starvation. This highlights a specific evolutionary adaptation in _Salmonella_.
    - **Clinical/Host Relevance:** Panel C is crucial for clinical microbiologists. It demonstrates that the exact same ribosomal depletion switch occurs when S.Tm is phagocytosed by macrophages. Inside the nutrient-restricted host vacuole, the bacteria actively shift into the 16Slow state, proving that this mechanism is directly relevant to intracellular survival and pathogenesis, not just a test-tube artifact.
- **Figure 3: Phenotypic Fitness During Nutritional Upshifts**
  - **What it shows:** This figure connects the physical state of the ribosomes to an evolutionary fitness advantage. It compares S.Tm populations subjected to carbon versus phosphate limitation, analyzing their rRNA-FISH distributions (Panel B) and active translation capacity using BONCAT (Panel C). Panels D, E, and F plot the lag times (the time it takes to resume growth) when these starved cells are transferred back into nutrient-rich media, at both the bulk and single-cell levels.
  - **Key Takeaways:**
    - **Condition-Dependent Bimodality:** Carbon starvation allows a distinct $16S^{high}$ subpopulation (about 16%) to persist, whereas phosphate starvation pushes almost the entire population into the depleted $16S^{low}$ state.
    - **Functional Translation:** The cells that maintain high rRNA levels (in carbon limitation) are not just hoarding inert ribosomes; BONCAT analysis proves they maintain significantly higher active protein synthesis rates.
    - **The Survival Advantage:** When nutrients are restored, the single-cell lag time distributions (Panel F) reveal a massive variance. The faster bulk recovery of the carbon-limited population is driven by a specific subset of "fast-recovery" cells. Strikingly, the percentage of these rapidly recovering cells perfectly mirrors the percentage of $16S^{high}$ cells, definitively linking the retention of ribosomes to a rapid-growth advantage.
- **Figure 4: Mechanistic Drivers (DksA and RNase I) and Phenotypic Proof**
  - **What it shows:** This is the mechanistic heart of the paper. Panel A and B visualize the Transposon Insertion Sequencing (TIS) screen, showing how the authors separated the 16Shigh and 16Slow populations to hunt for genetic drivers. Panels C and D use flow cytometry and microscopy to show what happens to rRNA levels when the identified genes (_dksA_ and _rna_) are knocked out (KO) or knocked down (KD) using CRISPR interference. Finally, Panels E and F plot the single-cell lag times of these mutants during a nutritional upshift.
  - **Key Takeaways:**
    - **The Genetic Drivers:** The TIS screen successfully isolated _dksA_ (transcription regulator) and _rna_ (encodes RNase I) as the genes highly enriched in the 16Shigh population.
    - **Abolishing the Bimodality:** Panel C provides striking visual proof: mutating either of these two genes completely prevents the formation of the 16Slow subpopulation. The cells are effectively trapped in the 16Shigh state.
    - **Tying Genotype to Phenotype:** Panels E and F brilliantly close the loop. Because the _dksA_ and _rna_ mutants cannot enter the 16Slow state, they lack the delayed recovery times seen in wild-type populations. As expected, these mutants exclusively exhibit the short, rapid lag times characteristic of the 16Shigh subpopulation, definitively linking the genetic mechanism to the evolutionary fitness advantage during nutrient restoration.

## Discussion and Implications

### Limitations

While the study elegantly connects single-cell transcriptomics to growth phenotypes, it presents certain limitations. The authors acknowledge that while they established correlation and genetic necessity (via knockouts), the exact mechanism causing only a _subset_ of cells to activate DksA/RNase I remains elusive. Furthermore, their mathematical model assumes a homogeneous starting population and cannot completely rule out alternate models where degradation rates are pre-assigned by an unknown bistable circuit rather than a stochastic switch.

### Evolutionary and Clinical Implications

Clinically, _Salmonella_ infections involve the bacteria invading and surviving inside host macrophages—a highly nutrient-restricted environment. The authors demonstrated that this exact ribosomal bimodality emerges when S.Tm infects J77A-1 macrophages.

The implications are profound for understanding bacterial persistence and antibiotic tolerance. Slow-growing or dormant subpopulations (like the 16Slow group) are notoriously tolerant to antibiotics, while the 16Shigh group serves as a rapid-response vanguard ready to exploit sudden nutrient availability in the gut. This bet-hedging strategy ensures that the population as a whole survives both acute starvation and antibiotic stress, while remaining highly competitive during feeding cycles. This innovation provides a mechanistic target (RNase I or DksA) for potential clinical therapies aimed at breaking bacterial dormancy to clear persistent infections.
