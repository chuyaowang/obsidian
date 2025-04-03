# BINN research proposal


## Background

- interpretation of DL models
- need for large amount of data
- Informed ML: use domain knowledge to reduce the _possible space of solutions_, while increasing interpretability

## Proposal

- Combines both biological modeling and ML models
- Investigate the claims that BINN produce more accurate and interpretable results by constructing and applying them in _several_ ways
- Uses ML, but not a ML project
- One approach: _follow_ the established techniques of using pathway datasets, such as the Reactome DB, as a source for cellular processes
- Also other knowledge sources, such as metabolic networks

## Implementation

- What biological information to use
- How to transform it into a NN architecture
- Depends on the data and problem
- Implementation in Python

## Validation

- Using transcriptomics data
- Other data types

## Transfer learning

- Does the parameters apply in other contexts?

## 

what is BINN

two uses of BINN:
- improve prediction, more interpretable
- discovery of new mechanisms from DL learning

important to define what to learn
what is the input and the output, what data, multi vs single omic
what we trying to learn


approaches

the underlying assumption: simpler means more interpretable?
	constraint that simplifies the network also a limit
	undiscovered connections, long range regulations, structural regulations, epigenetics, interconnections
does a NN that is cneected like a pathway network relally relfect the network? is it really comprehensive? what are the weights representing? how it explains data without this many features? does the interpreation of weights still hold? if it represents real biology, the weights should be the same! will it still make the correct predictions when missing features?

compare with FC NN
is NN really necessary or interpretable? a simplified NN is still complicated. needs more data. having many featuers also cause overfitting
does BINN really tell more than FCNN or simple ML? Elastic net example
counter intuitive to seek interpretability but hope 1 NN does everything
Do what we already know in already interpretable ways, and study what we don't know from interpretable NN.
separation of tasks, preprocessing before entering, using mroe interpresable approaches

Graph based approach: from the review
metDNA2: use multiple knwoledge networks for more comprehensive
cell oracle: no DL, just ML methods and even correlation
struc2vec: random walk in a multi-layer network; change the probability to be proportional to something else?
- what if we train the weights in a NN, VAE


validation
	
how to evaluate interpretability? 

![[Media/BINN research proposal 2025-03-24 12.24.17.excalidraw]]

drawbacks:

- supervisor is lecturer. weaker recommendation for PhD.
- not mainstream research direction: harder to find a PhD spot
- opportunity cost
- many uncertainties: the outcome, the publication,...