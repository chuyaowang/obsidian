# Statistical methods for polygenic risk scores in precision medicine

> Bogdan Pasaniuc, UCLA

Others:
> Bernie Berger
> Alkes Price

## Precision health

Aim: predict disease risk with genetic variants

### Problem

1. Reference population
2. Threshold for actionability
3. Ind A: high/low risk (This seminar)

## Polygenic scores (PGS)

- Phenotype = Genetics + Environmental factors;
- Hence, any genomic predictor has limited prediction accuracy;
- Common diseases are caused by many genomic variants;
- Polygenic score: summing genetic effects;
- A predictor that use genetic information to predict disease state![](Screenshot%202023-10-11%20at%2023.50.22.png)

### Terminologies

![](Screenshot%202023-10-11%20at%2023.51.49.png)

## Uncertainty in PGS

- When 2 and 3rd gene are correlated.
![](Screenshot%202023-10-11%20at%2023.54.34.png)

## Genetic ancestry impacts PGS error

- Genetic ancestry has arbitrary boundary;
- PGS accuracy is unknown for unclassified individuals;
- Self-identified ancestry makes it more diverse
- Instead of ancestry clusters, estimate individuals' genetic distance from training data;
- The further the distance, the lower accuracy PGS has.

## Non-genetic contexts impact PGS error

- Many contexts, known and unknown, affects PGS error;
- Calculate context-specific credible ranges;
- Use real biobank to calibrate the predictions;
- Large variations in individualized context-accuracy.

## Summary

![](Screenshot%202023-10-12%20at%2000.30.42.png)