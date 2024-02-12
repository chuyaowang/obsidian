# Single Cell Metabolomics

## Intro

Previously metabolomics is only available at the cell population level. Lipids, carbohydrates, small molecules are dynamic and different in every cell, and efforts are made to study them in single cell resolutions.

Speakers:
- Theodore Alexandrov, EMBL
- Anne Le, Gigantest

## Why single cells

Metabolism is different in every cell. In cell therapies where immune cells are introduced, the metabolism of one cell will determine the phenotype of all the cells that derive from it. Just like single cell RNA-seq, at the single cell resolution, a lot of new mechanics can be uncovered. 

In disease diagnosis, treatment, and drug discovery, understanding single cell metabolism will help differentiate normal cells from disease cells such that targeted therapies can be tailored.

For example, circulating cancer cells are hard to detect in blood samples. If they can be detected however, cancer can be diagnosed much earlier.

## Challenges

### Challenges

- When a cell is isolated from its population for analysis, its neighboring environment changes, which will also change its metabolism.
- Bulk metabolomics requires 1 million cells to start with. Having enough material for detection constitutes another problem in single cell metabolomics.
- Lack of amplification: in DNA or RNA sequencing, the sequence can be amplified to reach the detection limit, but in metabolomics no amplification method has been developed.
- Metabolites can diffuse out of the cell membrane. Cell preparation and isolation protocols should be developed to introduce as little stress as possible.
- Controlling for and understanding the non genetic factors that influence the metabolome.
- Metabolic dark matter: much of the data cannot be annotated. Using [imaging mass spectrometry](Imaging%20Mass%20Spectrometry), 100 Gbs of data can be collected from tissue sections, but the metabolites that can be identified constitutes less than 10 Mbs. 

### Perspectives

- Fundamental understanding of analytical chemistry: how the signals are generated from the material; how molecular ionization takes place.
- Computational methods: model how signals are created from chemical structures; generative models that generate peaks given a molecule.
- Tracing where does the metabolite come from to give actionable therapy advice: if someone's blood sugar is high, where does the sugar come from and how to reduce it.

## Proteomics and metabolomics

- Having protein expression does not 100% lead to reaction involving metabolites.
- Structural diversity of the metabolome makes it difficult to have one protocol that detects everything, whereas the protocol for proteomics is pretty much set despite also having structural diversity.
- Metabolites can be affected by genetic and non-genetic factors, introducing new challenges in computational methods to identify metabolites.
	- Impossible protein: a protein sequence that is randomly shuffled while preserving the k-let counts (the frequencies of k consecutive letters) of the original sequence. This approach is used to evaluate the statistical significance of a biological sequence by comparing it with a large sample of random sequences. For example, if you want to annotate or identify a protein based on its sequence similarity with known proteins, you can use the impossible protein as a negative control to test the validity of your method
	- In metabolomics, the structural diversity is much greater than what sequence shuffling can model.

## Applications

### Cancer

- Tumor microenvironment, immune cell metabolism, and their interactions.
- Cancer is not only controlled by gene but also the metabolome: exposure to diabetic metabolic environment induced cancer in healthy pancreatic cancer cells. The gene, protein, diet, lifestyle, environment collectively determine the metabolic environment.
- Research on metabolic competition between cancer and immune cells; immune metabolism.
- Distinguish cancer and immune cells to deliver targeted therapy.

### Health and disease

- Metabolic disorder underpins many dieases: Warburg effect observed in other types of diseases.
- Drug development: how is the drug metabolized; how is adverse effect created.
- Therapy selection and monitoring: using organoids to select drugs with the least adverse effects.
- Cell therapy: immune cell function is linked to metabolic state. Adaptive cell therapies can be optimized not only genetically but also metabolically to achieve greater effect in vivo.
- Diagnostics using liquid biopsies.
- Single cell metabolomics, being the cheapest omics technology, have the potential for developing into a data source for drug selection. AI can be used to generate drug structures from metabolic structure atlases. 