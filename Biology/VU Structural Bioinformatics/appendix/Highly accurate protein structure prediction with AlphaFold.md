# AlphaFold

#paper 
[link](https://www.nature.com/articles/s41586-021-03819-2)

## Abstract

- AlphaFold2: structure prediction without homologs
- physical and biological knowledge, multiple sequence alignment, deep learning

## Introduction

- Two distinct approaches of structure prediction
	- From **simulation of molecular physics**: theoretically sound but computationally intractable
	- From evolutionary history of proteins, homology to **solve structures**, and pairwise evolutionary correlations
- AF2 can predict structure without homologous structures
- High back-bone and all-atom accuracy
- Provides per-residue estimate of prediction reliability

## AlphaFold Network

### Information flow

![](Pasted%20image%2020250217130618.png)
![](Media/Pasted%20image%2020250219121647.png)
- $s$, number of sequences (N_seq in the main text); 
- $r$, number of residues (N_res in the main text); 
- $c$, number of channels.

### The AF2 network

- evolutionary, physical and geometric constraints of protein structures
1. **Multiple Sequence Alignments (MSAs)**:
   - **Definition**: An arrangement of protein or nucleic acid sequences to identify regions of similarity.
   - **Purpose**: These alignments help infer evolutionary, structural, or functional relationships.

2. **Pairwise Features**:
   - **Definition**: Characteristics derived from comparing pairs of sequences.
   - **Purpose**: These features help understand relationships between two sequences in terms of their structural and functional similarities.

3. **Output Representation and Associated Loss**:
   - **Output Representation**: The format in which the predicted protein structure is presented.
   - **Associated Loss**: A measure of how accurately the predicted output matches the true structure.
   - **Purpose**: This helps in training the neural network to minimize errors in prediction.

4. **Equivariant Attention Architecture**:
   - **Definition**: A neural network design that maintains spatial relationships in 3D space.
   - **Purpose**: Ensures that the network's attention mechanism is aware of geometric transformations, leading to more accurate structural predictions.

5. **Intermediate Losses**:
   - **Definition**: Loss values calculated at various stages during the network's iterative refinement process.
   - **Purpose**: Helps in progressively improving the accuracy of predictions at each stage.

6. **Masked MSA Loss**:
   - **Definition**: A training technique where parts of the MSA are hidden (masked) to encourage the network to learn underlying patterns.
   - **Purpose**: Improves the network’s ability to generalize by focusing on learning evolutionary relationships without overfitting.

7. **Self-Distillation**:
   - **Definition**: A training method where a model is retrained on its own high-confidence predictions.
   - **Purpose**: Enhances accuracy by leveraging predictions on unlabelled sequences.

8. **Self-Estimates of Accuracy**:
   - **Definition**: The model’s own predictions about how accurate its outputs are.
   - **Purpose**: Provides confidence levels for the predicted structures, helping users assess reliability.

### Rewritten Sentence (Fixed Run-On)
"In particular, we demonstrate a new architecture to jointly embed multiple sequence alignments (MSAs) and pairwise features. This includes a new output representation and associated loss that enable accurate end-to-end structure prediction, a new equivariant attention architecture, and the use of intermediate losses to achieve iterative refinement of predictions. Additionally, we employ masked MSA loss to jointly train with the structure, along with learning from unlabelled protein sequences using self-distillation and self-estimates of accuracy."
