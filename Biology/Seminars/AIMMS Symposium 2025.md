# AIMMS Symposium 2025

#seminar 

Act as an experienced subject expert in systems biology, constraint based modeling, and modeling of metabolic networks. Read the provided transcribed text of a talk in the Amsterdam Institute of Molecular and Life Sciences Symposium. First understand what the given text is about and delineate its logical flow. Understand what are the sections or topics discussed of the talk. Then for each part summarize the challenges resolved, methods used, the results, and how it leads to the next section. If it is a panel, then for each topic synthesize the views presented by each panelist. Be detailed and provide context in the sectional summaries. Focus on technical descriptions. Also summarize each question asked and the answers in the Q&A session in the end if there is one. Generate the contextual knowledge needed to understand the topics discussed and questions asked. Finally give a comprehensive summary of the text: what was the motivation, research question or central argument, the conclusion, the current limitations, alternative perspectives, and what are the potential next steps. Save the output to a markdown file with an informative name related to the talk.

Here is information about the talk:
- Title: E Coli is Protein-Saturated: Lessons Learned from an Improved Enzyme Constraint Based Model
- Speakers: 
	- Claudia de Buck, Wageningen University
- Transcribed text: 
- In addition, keep in mind that this is a machine produced transcribed text so there may be mistakes. If you change any transcribed text in the summary, note the change.

## Constraint Based Models to Understand and Design Microbial Co-Cultures for C1 Utilization

> Maria Suarez Diez, Wageningen University & Research

syngas: CO, CO2 H2

wood-ljundahl pathway


![](Media/Recording%2020251031132944.m4a)

## Dual Substrate Uptake can Release Metabolic Limitations Leading to Improved Synergistic Yields: Metabolic Interactions between Different Substrates

> Timmy Paez-Watson, Technische Universiteit Delft


![](Media/Recording%2020251031135056.m4a)


## Beyond Real Species. Random Metabolisms as a New Lens to Microbial Community Ecology

> Djordje Bajic, Technische Universiteit Delft
> [Review: Structuring complexity by mapping the possible in microbial ecosystems](https://www.sciencedirect.com/science/article/pii/S1369527425000803) 


![](Media/Recording%2020251031141522.m4a)

## E Coli is Protein-Saturated: Lessons Learned from an Improved Enzyme Constraint Based Model

> Claudia de Buck, Wageningen University

![](Media/Recording%2020251031142856.m4a)

## Decoding fermentation: how redox interconversions explain Clostridium Pasteurianum activity

> Wessel de Kok, Technische Universiteit Delft




> Challenges

## Challenges of a Vast Solution Space in GEMs

> Ursula Kummer, BioQuant, Heidelberg University



- whole genome scale metabolic models
- large solution space for FBA
	- [4. VU ISB Stoichiometric Models of Metabolism](Biology/VU%20Introduction%20to%20Systems%20Biology/4.%20VU%20ISB%20Stoichiometric%20Models%20of%20Metabolism.md)
	- steady state solution -> flux vectors
- Null space $Nv=0$ is the null space of N
- FBA gives the optimal solution
- FBA for E. faecalis, lactic acid bacterium
- Construction of stoichiometric networks of E. faecalis
	- based on genome annotations and existing modes
	- manual curation
	- addition of transporters
- Automatic tools:
	- does not work for all problems
	- Agora, KBase, PubSEED, CarveME, Merlin, and MetaDraft
- FBA applied to E. faecalis
	- incorrect predictions due to kinetic effects
- complement with other omics
	- often only transcriptomics
	- proteomics often incomplete
	- poor correlation between proteomic and transcriptome
	- labor extensive experiments
- idea
	- SWATH-MS - proteome measurements
	- quantitative proteome data to further constrain GSMs
- ph-shift experiment
	- slow reduction of pH
	- samples at diff time points
	- steady state at pH 7.5 and 6.5
- include protons in the model
	- inclusion of reactions and transporters that influence pH
	- increase ATP demand with decreasing pH
	- amino acid uptake for ATP generation
- proteome data
	- non detected: remove reaction
	- reactivation of essential proteins with limits
	- incorporate of fold changes in constraints
- predicted changes in flux
	- still have uncertainty
- how to address remaining uncertainty
	- FVA flux variability analysis, but hard to interpret w.r.t. phenotypes
	- CoPE-FBA: see the solution space as a combination of metabolic subnetworks
	- Perturbation approach. fix one flux at values within interval then calculate flux distributions
- Undetermined flux distributions
- conclusions
![](Media/Recording%2020251031153909.m4a)

## Parametrizing protein allocation models how evolution shapes enzyme turnover numbers to support cellular objectives

> Samira van den Bogaard, RWTH Aachen University

- enzyme efficiency
- extracellular environment - intracellular kinetics
- open questions
- assumptions (considerations)
	- optimize growth
	- proteomes can be partitioned
	- not all proteins are fully used
- protein allocation models (PAMs)
	- Protein constrained model
	- metabolic model
- enzyme evolution on computer
- kcat distribution is conserved 


![](Media/Recording%2020251031155259.m4a)


## Coexistence in microbial communities: the role of metabolites and toxins

> Meike Wortel, University of Amsterdam

- frequency dependent selection
	- intra-species competition
	- niche creation (cross feeding, detoxification)
	- trade-offs: can't be good at everything (Darwin demon)
- Fluctuating environments maintain coexistence
- Cross protection lead to coexistence


![](Media/Recording%2020251031162230.m4a)

## alkaline ph driven metabolic plasticity of Lactococcus lactis FM03


![](Media/Recording%2020251031163923.m4a)



