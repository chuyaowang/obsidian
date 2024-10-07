# BLOSUM62

[Where did the BLOSUM62 alignment score matrix come from](https://www.nature.com/articles/nbt0804-1035)

Blocks of conserved regions in aligned protein sequences are used to compute the scores. For BLOSUM62, the blocks contain sequences with up to 62% identity.

The scores in the matrix reflect the likelihood of amino acid substitutions during evolution, computed as log odds ratios between the observed probability and the expected probability of the substitutions:
$$
\mathrm{S(i,j)} = \frac{1}{\lambda}\log(\frac{P(i,j)}{E(i,j)}),\quad\mathrm{S}\in Z
$$
, where $P(i,j)$ is the observed substitution probability between amino acids $i$ and $j$ calculated from known aligned protein sequences, $E(i,j)$ is the likelihood of the null hypothesis, calculated from the background frequencies of $i$ and $j$ in any protein sequences, and $\lambda$ is a scaling factor that rounds the scores to integers. 

A positive value suggests the amino acids have more frequently substituted each other than random chance. Hence, the substitution is likely benign. Oppositely, a negative value means the substitution is likely deleterious. A higher absolute value of the scores indicates a more benign/deleterious substitution.

BLOSUM62 is the default matrix for [The BLAST Algorithm](3.%20MIT%20CompBio%20-%20Hashing,%20Database%20Search,%20BLAST%20algorithm.md#The%20BLAST%20Algorithm%20and%20Inexact%20Matching). It is used to compute neighborhood similarity in step 2 and sequence similarity in step 4 (See linked notes).