# Confusion Matrix

## Confusion Matrix

|                    | Real Positive       | Real Negative       |
| ------------------ | ------------------- | ------------------- |
| Predicted Positive | True Positive (TP)  | False Positive (FP) |
| Predicted Negative | False Negative (FN) | True Negative (TN)  |

## True Positive Rate (TPR) / Sensitivity / Recall

- Measures the proportion of actual positives correctly identified.
- $\text{TPR} = \frac{\text{TP}}{\text{TP} + \text{FN}}$
- **Interpretation**: Measures the ability to correctly label actual positives as positives, indicating the model's ability to detect actual positives.

## False Positive Rate (FPR)

- Measures the proportion of actual negatives incorrectly identified as positives.
- $\text{FPR} = \frac{\text{FP}}{\text{FP} + \text{TN}}$
- **Interpretation**: Measures the rate at which false alarms occur. A lower FPR indicates that fewer incorrect positive predictions are made.

## True Negative Rate (TNR) / Specificity

- Measures the proportion of actual negatives correctly identified.
- $\text{TNR} = \frac{\text{TN}}{\text{TN} + \text{FP}}$
- **Interpretation**: Measures the ability of the test to correctly identify negatives. Higher TNR (Specificity) means fewer false positives.

## Positive Predictive Value (PPV) / Precision

- Measures the proportion of positive predictions that are true positives.
- $\text{PPV} = \frac{\text{TP}}{\text{TP} + \text{FP}}$
- **Interpretation**: Measures the proportion of positive predictions that are actually correct. Higher PPV means that when the test predicts a positive, it is more likely to be correct.

These metrics provide a comprehensive understanding of the performance of a binary classifier by evaluating both its ability to correctly identify positive cases and its ability to correctly reject negative cases.
