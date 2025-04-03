# Beyond the black box with biologically informed neural networks

[paper link](https://www.nature.com/articles/s41576-025-00826-1)
#paper 

## Intro

- ML models are used for prediction tasks using multi-omic data. However, their explainability is limited.
- **Biologically informed neural networks (BINN)** combines predictive accuracy with explainability by incorporating prior biological knowledge.
	- Neural network can fit anything. Accuracy from overfitting or truly learned insight? 
	- Having many features can also cause overfitting, not just have a complex network. What happens if they do a feature selection prior to entering the network?
- Understanding model predictions based on _complex, high dimensional_ multimodal datasets found in _multi-omics integration_

## From black boxes to visible neural networks

- BINN's architecture (nodes and layers) is constrained by pathway ontologies.
- Node: a biological entity, like a gene, pathway or biological process
- Edge: a known relation; a gene is only connected to a pathway if it belongs to the pathway
- Advantages:
	- reduces number of model parameters
	- intuitive to researchers
	- mitigates overfitting and increases generalizability (doubtfully, could still be too many parameters even after reduced)
	- connects data-driven models to mechanistic biological understanding
- My thoughts:
	- is reducing complexity of the network really not an over-simplification? Is $\text{Simplicity}=\text{Explainability}$ necessarily true?
	- are pathway connection reflective of all the regulatory connections; some regulations may be subtle, structural, epigenetic. Are these reflected?
	- long range feedback control reflected in this schematic?
	- what about undiscovered control mechanism?
	- clearly limited and does not help discovering new knowledge. what exactly are we trying to learn by explaining the NN here?
	- what do the weights represent then?
	- representing interconnections: genes regulate proteins but proteins also regulate genes

## Applications

- Introduction in 2018
- P-Net: aligning _molecular features_ to therapeutic outcomes
- Integrated _genomics data_ with _chemical structure data_ to predict therapeutic accuracy
- Multi-omics data and clinical data to predict patient survival (bruh)
- Biologically informed VAE: analyze cellular processes and aid in drug development (aid, huh)
- Cellular heterogeneity and regulatory networks from [scRNA-seq](Biology/Concepts/scRNA-seq.md)
- Discover novel pathway interactions
- My thoughts:
	- Important to define what inputs we are using and what we are trying to predict
		- does it have to be multi omics?
	- Again, what we are trying to learn by explaining the NN?
		- what factors are contributing to what phenomenon?
	- Maybe don't need to aim to do everything using a neural network? Divide the task and use more interpretable methods to do most parts, like [Dissecting cell identity via network inference and in silico gene perturbation](Biology/Seminars/Dissecting%20cell%20identity%20via%20network%20inference%20and%20in%20silico%20gene%20perturbation.md).
		- Do what we already know in already interpretable ways, and study what we don't know from interpretable NN.
		- also AF2 that uses MSA, which is interpretable and based on biological knowledge.
	- graph approach in [Identifying maximally informative signal-aware representations of single-cell data using the Information Bottleneck](Biology/Seminars/Identifying%20maximally%20informative%20signal-aware%20representations%20of%20single-cell%20data%20using%20the%20Information%20Bottleneck.md)

## BINN for multi-omics data integration

 - high-dimensional, heterogeneous and often limited in sample size relative to the number of features
 - BINN has fewer connections, so less model complexity, more generalizability
 - Comparative performance to FC NN (seriously?) for small, high-dimensional dataset (so for large high dimensional it doesn't?)
 - Capture non-linear, hierarchical relationship compared to traditional ML (of course, traditional ML is not good at this)
 - BINN is more interpretable because predictions are directly linked to nodes, which are linked to biological entities
 - My thoughts:
	 - Do feature selection before sending them to NN?
	 - meaning the structure is fixed and cannot adapt to other data without some features? where is the generalizability here?
		 - is the goal to predict on new data or to interpret the learned weights?
		 - Use BINN to make better predictions or learn the mechanism by interpreting the weights?

## Advancing BINNs for biomedical discovery

- Challenges:
	- narrow task range and datasets
	- unclear reason for superior performance
	- lack of benchmarking, like CASP
- Future:
	- more diverse architecture
	- more robust construction and evaluation
	- more advanced multi-modal fusion strategies and systematically exploring the impact of different ontologies
	- BINN for hypothesis generation, such as predicting novel pathway relationships (can we really not do this with link prediction in GNN?)
- My thought:
	- wild thought: use another NN to classify nodes and edges of an uninterpretable NN?
	- validation method: how do known biomarkers perform in the interpreted results of BINN? compare with FC NN
	- VAE: encoder learns weights, weights are used for GRN inference in the middle, GNN as decoder layer to reconstruct data. GNN can be visualized.
	- [Metabolite annotation from knowns to unknowns through knowledge-guided multi-layer metabolic networking](Biology/Seminars/Metabolite%20annotation%20from%20knowns%20to%20unknowns%20through%20knowledge-guided%20multi-layer%20metabolic%20networking.md): use multiple different networks to capture different aspects of biology simultaneously