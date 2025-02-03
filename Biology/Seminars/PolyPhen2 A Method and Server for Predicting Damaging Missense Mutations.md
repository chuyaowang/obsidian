# PolyPhen2

#paper 
[Paper link](https://www.nature.com/articles/nmeth0410-248)

Predicts the damaging effects of [missense mutations](2.%20VU%20FoB%20-%20Mutation,%20Evolution,%20and%20Sequence%20Alignment.md#Mutation), like [SIFT](SIFT%20Predicting%20Amino%20Acid%20Changes%20that%20Affect%20Protein%20Function.md)

PolyPhen2 uses 8 sequence-based and 3 structure-based predictive features, selected with an iterative [Greedy Algorithm](Greedy%20Algorithm.md).

## PolyPhen2 vs. PolyPhen

Naive bayes classifier.
Different features.

## Training Data

PolyPhen2 has two flavors trained on two sets of data, suitable for different tasks.

### HumDiv

- **Damaging**: all 3155 damaging alleles annotated in the [UniProtKB](UniProtKB.md) database as causing human [Mendelian Diseases](Mendelian%20Diseases.md) and affecting protein stability or function.
- **Benign**: 6321 differences between human proteins and their closely related mammalian [homologs](2.%20VU%20FoB%20-%20Mutation,%20Evolution,%20and%20Sequence%20Alignment.md#Homology) (homologs from cows or chimpanzees, for example).
	- This could cause issues as mutations could have different biological implications for protein homologs in different animals.
	- Damaging/benign mutation in one species may not act the same in another species.
	- Presence of redundant pathways, regulatory mechanisms, different reactions, etc. can cause this difference.

Suitable for _rare alleles_ at loci potentially involved in complex phenotypes, for dense mapping of regions identified by genome-wide association studies and for analysis of natural selection from sequence data, in which even mildly deleterious alleles must be treated as damaging.

### HumVar

- **Damaging**: All 13032 human disease-causing mutations from [UniProtKB](UniProtKB.md).
- **Benign**: 8946 human nonsynonymous [Single Nucleotide Polymorphism](Single%20Nucleotide%20Polymorphism.md)s (nsSNPs) without annotated involvement in disease.

The nsSNPs of the HumVar dataset, which are assumed to be benign, include a sizable fraction of **mildly deleterious** alleles.

Diagnostics of _Mendelian_ diseases require distinguishing mutations with drastic effects from other human variation, including abundant mildly deleterious alleles, 


