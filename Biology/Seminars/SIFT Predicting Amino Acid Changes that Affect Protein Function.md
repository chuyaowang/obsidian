# SIFT

#paper 

## Introduction

SIFT predicts whether a missense [Mutation](2.%20VU%20FoB%20-%20Mutation,%20Evolution,%20and%20Sequence%20Alignment.md#Mutation) is deleterious.

It relies solely on the sequence for prediction. No structural information is used.

## Prediction Method

[SIFT predicting amino acid changes that affect protein function (2003)](SIFT%20predicting%20amino%20acid%20changes%20that%20affect%20protein%20function.pdf)

A key assumption is that important amino acids are conserved during evolution. So changes in these regions tend to be deleterious.

For example, if in multiple similar proteins, the amino acid at position $x$ is a isoleucine, then it is likely changing it to other amino acids will be deleterious. Similar rules can be made for hydrophobic amino acids, hydrophilic amino acids, etc.

SIFT first aligns the query sequence to protein sequences in the database. It uses two rounds of PSI-BLAST to achieve this.

It then clusters sequences with higher than 90% identity into one group. [PSI-BLAST](2.%20VU%20FoB%20-%20Mutation,%20Evolution,%20and%20Sequence%20Alignment.md#PSI-BLAST) is run iteratively within the group until a median conservation threshold is reached.

Based on the amino acids appearing at each position in the alignment, SIFT calculates the probability that an amino acid at a position is tolerated conditional on the most frequent amino acid being tolerated. If this normalized value is less than a cutoff, the substitution is predicted to be deleterious.

A score less than 0.05 is predicted to be deleterious.

## SIFT 4G

[SIFT missense predictions for genomes (2016)](https://www.nature.com/articles/nprot.2015.123)

SIFT 4G is a GPU implementation of SIFT, faster and with several improvements.

### Step 1: Search for similar sequences against a large protein database

First, similar sequences are identified by [Seed Detection](Seed%20Detection.md) followed by a GPU implementation of the [Smith-Waterman Algorithm](3.%20MIT%20CompBio%20-%20Hashing,%20Database%20Search,%20BLAST%20algorithm.md#Smith-Waterman%20Algorithm). This is different from what SIFT does, which is two rounds of PSI-BLAST. This is much faster but slightly less sensitive to distantly related homologous sequences.

SIFT uses protein sequence databases such as [UniProtKB/SWISS-PROT](UniProtKB.md) to search for similar sequences.

#### Seed detection

Say we have a query sequence and some database sequences. Seed detection is done by first dividing each sequence into overlapping k-mers. Then matching k-mers are found across the sequences. Their indices are recorded in a new list.

For example, for one sequence it is `[1, 3, 7, 9, 12]`, and for another is `[2, 4, 10, 8, 14]`. Meaning the 1st k-mer in the query sequence matches the 2nd k-mer in the database sequence, and so on.

Then the [Longest Increasing Subsequence (LIS) algorithm](Longest%20Increasing%20Subsequence%20Problem.md) is used to find the LIS in the lists. The algorithm works by finding the longest subsequence where the positions of the matching k-mers **increase in both sequences**. For a subsequence to be valid in the context of LIS, the relative positions of the k-mers must be in the same order in both the query and the database sequence.

So the LIS in this example is `[1,3,7,12]` and `[2,4,10,14]`. Since `8` does not increase from `10`, `9` after `7` is also not counted.

The length of LIS is used as the similarity score. The top 5000 sequences with the highest similarity score is passed to the next step.

#### Smith-Waterman Algorithm

The local alignment algorithm reconstructs the alignment between the query and the top 5000 hits, of which 400 sequences with the most significant p values are kept.

At this point, the query protein sequence is aligned to its homologous sequences.

### Step 2: Choose closely related sequences

#### Median Conservation

Described in [Accounting for human polymorphisms predicted to affect protein function (2002)](https://pubmed.ncbi.nlm.nih.gov/11875032/)

Conservation, as measured by information content ([Schneider et al. 1986](https://genome.cshlp.org/content/12/3/436.long#ref-31)), is calculated for each position in the alignment, and the median of these values is obtained. 

The median conservation can range from 4.3 (sequences nearly 100% identical to each other) to 0 (all 20 amino acids are represented at the majority of positions in the sequence alignment). 

#### Choosing consensus sequences

Consensus sequences are sequences that are similar to each other.

In the original SIFT, consensus sequences were found by first clusters sequences with over 90% identity into clusters. Then [PSI-BLAST](2.%20VU%20FoB%20-%20Mutation,%20Evolution,%20and%20Sequence%20Alignment.md#PSI-BLAST) was run iteratively until the chosen consensus sequences reached the [sequence Median Conservation threshold](#Median%20Conservation).

In SIFT 4G, this step is simplified by removing the clustering step. The 400 sequences from the first step are added iteratively. The most significant hits are added first until the median sequence conservation is reached (the default is 2.75, set by the authors). Still uses PSI-BLAST.

### Step 3: Calculate probabilities for amino acid substitutions

Multi-thread implementation, otherwise changed.

[Predicting Deleterious Amino Acid Substitutions (2001)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC311071/) describes how exactly are the scores calculated from here. [PSSM](2.%20VU%20FoB%20-%20Mutation,%20Evolution,%20and%20Sequence%20Alignment.md#PSSM) from the alignment result from the previous step is used.

$$
p_{ca} = \frac{N_c}{N_c+B_c}\cdot g_{ca} + \frac{B_c}{N_c+B_c}\cdot f_{ca}
$$
$N_c$: total number of sequences in the alignment
$g_{ca}$: the (sequence-weighted) frequency that amino acid $a$ appears at position $c$ in the alignment
$f_{ca}$: pseudocounts, calculated from a 13-component Dirichlet mixture
$B_c$: total number of pseudocounts

$p_{ca}$: the estimated probability of amino acid $a$ appearing at position $c$
- low $p_{ca}$: it is unlikely, so if it appears, it is likely damaging
$p_{ca}$ is normalized on the consensus amino acid in each column, which is the amino acid with the highest $p_{ca}$

Pseudocounts take into account other amino acid sequences not included in the database but are similar enough to be one of the [consensus sequences](#Choosing%20consensus%20sequences).
Pseudocounts: a prior estimate, such that low count statistics are not going to have any extreme effects.

## Score

Ranges from 0 to 1
Damaging: 0
Benign: 1

Cutoff at 0.05: for 95% confidence.