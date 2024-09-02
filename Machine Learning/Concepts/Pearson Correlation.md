# Pearson Correlation

The Pearson correlation coefficient is a measure of the **linear relationship** between two vectors (or sets of data). It quantifies how much one variable changes in response to changes in another variable, giving both the direction and the strength of the relationship.

### Definition

Given two vectors $\mathbf{x}$ and $\mathbf{y}$ of length $n$, the Pearson correlation coefficient $r$ is defined as:

$r = \frac{\sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum_{i=1}^{n} (x_i - \bar{x})^2} \sqrt{\sum_{i=1}^{n} (y_i - \bar{y})^2}}$

where:
- $x_i$ and $y_i$ are the individual elements of the vectors $\mathbf{x}$ and $\mathbf{y}$, respectively.
- $\bar{x}$ and $\bar{y}$ are the means of the vectors $\mathbf{x}$ and $\mathbf{y}$, respectively.

### Interpretation

1. **Value Range**: The Pearson correlation coefficient $r$ ranges from -1 to 1.
   - $r = 1$: Perfect positive linear relationship. As one variable increases, the other variable increases proportionally.
   - $r = -1$: Perfect negative linear relationship. As one variable increases, the other variable decreases proportionally.
   - $r = 0$: No linear relationship. Changes in one variable do not predict changes in the other variable.

2. **Strength of Relationship**:
   - $|r|$ close to 1: Strong linear relationship.
   - $|r|$ close to 0: Weak or no linear relationship.

### What Pearson Correlation Tells Us

1. **Direction**: The sign of $r$ indicates the direction of the relationship:
   - Positive $r$: Both variables tend to increase together.
   - Negative $r$: One variable tends to decrease as the other increases.

2. **Strength**: The magnitude of $r$ indicates the strength of the relationship:
   - Values close to 1 or -1 indicate a strong linear relationship.
   - Values close to 0 indicate a weak linear relationship.

3. **Linearity**: Pearson correlation specifically measures the strength and direction of a linear relationship. It does not capture non-linear relationships.

### Example

Consider two vectors $\mathbf{x} = [1, 2, 3, 4, 5]$ and $\mathbf{y} = [2, 4, 6, 8, 10]$:

1. Compute the means:
   $\bar{x} = \frac{1 + 2 + 3 + 4 + 5}{5} = 3, \quad \bar{y} = \frac{2 + 4 + 6 + 8 + 10}{5} = 6$

2. Compute the covariance:
   $\sum_{i=1}^{5} (x_i - \bar{x})(y_i - \bar{y}) = (1-3)(2-6) + (2-3)(4-6) + (3-3)(6-6) + (4-3)(8-6) + (5-3)(10-6) = 20$

3. Compute the standard deviations:
   $\sqrt{\sum_{i=1}^{5} (x_i - \bar{x})^2} = \sqrt{(1-3)^2 + (2-3)^2 + (3-3)^2 + (4-3)^2 + (5-3)^2} = \sqrt{10}$
   $\sqrt{\sum_{i=1}^{5} (y_i - \bar{y})^2} = \sqrt{(2-6)^2 + (4-6)^2 + (6-6)^2 + (8-6)^2 + (10-6)^2} = \sqrt{40}$

4. Compute $r$:
   $r = \frac{20}{\sqrt{10} \cdot \sqrt{40}} = \frac{20}{\sqrt{400}} = \frac{20}{20} = 1$

This indicates a perfect positive linear relationship between $\mathbf{x}$ and $\mathbf{y}$.

### Caveats

- **Linearity**: Pearson correlation measures linear relationships only. If the relationship is non-linear, $r$ might be close to 0 even if there is a strong relationship.
- **Outliers**: Sensitive to outliers, which can disproportionately affect the correlation.
- **Assumption of Normality**: Assumes the data is _normally distributed_, though it can still be used for non-normal data with caution.

In summary, the Pearson correlation coefficient provides a concise measure of the direction and strength of the linear relationship between two vectors. It is widely used in statistics and data analysis to understand the relationship between variables.