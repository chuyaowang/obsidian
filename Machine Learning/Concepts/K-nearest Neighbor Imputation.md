# KNN Imputation

K-Nearest Neighbor (KNN) imputation is a technique used to fill in missing values in a dataset by leveraging the similarity between instances. The basic idea is to find the 'k' closest instances (neighbors) to the instance with the missing value and use these neighbors to estimate the missing value. Here’s a step-by-step explanation of how KNN imputation works:

1. **Identify Missing Values**: Determine which data points in the dataset have missing values.

2. **Choose a Distance Metric**: Select a distance metric to measure the similarity between instances. Common choices include Euclidean distance, Manhattan distance, and cosine similarity. The choice of metric can influence the imputation results.

3. **Find K Nearest Neighbors**: For each instance with a missing value, find the 'k' nearest neighbors that have complete data (i.e., no missing values for the relevant attributes).

4. **Compute Imputation Value**:
   - **Numerical Data**: For numerical attributes, the missing value is often imputed by taking the mean, median, or a weighted average of the corresponding attribute values from the 'k' nearest neighbors. The weighted average might use the inverse of the distance as weights.
   - **Categorical Data**: For categorical attributes, the missing value can be imputed by taking the mode (most frequent value) of the corresponding attribute values from the 'k' nearest neighbors.

5. **Replace Missing Values**: Substitute the missing value with the imputed value derived from the 'k' nearest neighbors.

### Example

Suppose we have a dataset with three features \( F1, F2, \) and \( F3 \), and we want to impute the missing value in \( F3 \) for a particular instance:

| F1  | F2  | F3  |
|-----|-----|-----|
| 5.1 | 3.5 | 1.4 |
| 4.9 | 3.0 | 1.4 |
| 4.7 | 3.2 | 1.3 |
| 4.6 | 3.1 | NaN |
| 5.0 | 3.6 | 1.4 |

1. **Identify Missing Value**: The missing value in the fourth instance for \( F3 \).

2. **Choose Distance Metric**: Use Euclidean distance. We only use \( F1 \) and \( F2 \) for calculating distance since \( F3 \) has the missing value.

3. **Find K Nearest Neighbors**: Suppose \( k=3 \). Compute distances from the fourth instance to all other instances:
   - Distance to (5.1, 3.5): \(\sqrt{(5.1-4.6)^2 + (3.5-3.1)^2} = 0.64\)
   - Distance to (4.9, 3.0): \(\sqrt{(4.9-4.6)^2 + (3.0-3.1)^2} = 0.31\)
   - Distance to (4.7, 3.2): \(\sqrt{(4.7-4.6)^2 + (3.2-3.1)^2} = 0.14\)
   - Distance to (5.0, 3.6): \(\sqrt{(5.0-4.6)^2 + (3.6-3.1)^2} = 0.64\)

4. **Select the Nearest Neighbors**: The three nearest neighbors are (4.7, 3.2), (4.9, 3.0), and either (5.1, 3.5) or (5.0, 3.6).

5. **Compute Imputation Value**: Take the mean of \( F3 \) values for these nearest neighbors:
   - Neighbors' \( F3 \) values: 1.3, 1.4, 1.4
   - Mean: \( (1.3 + 1.4 + 1.4)/3 = 1.37 \)

6. **Replace Missing Value**: Impute \( F3 \) in the fourth instance with 1.37.

### Advantages and Disadvantages

**Advantages:**
- Simple to understand and implement.
- Works well when data has a strong local structure.

**Disadvantages:**
- Computationally intensive for large datasets.
- Requires a careful choice of 'k' and distance metric.
- Assumes that the distance metric used is appropriate for the data's distribution and relationships.

KNN imputation is a powerful method when used correctly, especially in cases where the local patterns in the data are informative.