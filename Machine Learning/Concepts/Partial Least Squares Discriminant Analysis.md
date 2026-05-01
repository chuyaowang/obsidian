# Partial Least Squares Discriminant Analysis (PLS-DA) and its Variants

This document provides a technical deep-dive into the Partial Least Squares (PLS) family of algorithms. These methods are essential for high-dimensional data analysis where the number of variables ($p$) often exceeds the number of samples ($n$), and multicollinearity (highly correlated features) is present.

---

## 1. The Core Engine: Partial Least Squares (PLS)

### PCA vs. PLS-DA
*   **PCA (Principal Component Analysis)**: A **unsupervised** method. It seeks directions (Principal Components) that capture the maximum **variance** within the feature matrix ($X$). It does not know about your classes ($Y$).
*   **PLS-DA**: A **supervised** version. It seeks directions (Latent Components) that maximize the **covariance** between the feature matrix ($X$) and the class membership matrix ($Y$). It actively looks for features that explain the differences between your groups.

### Key Components of the Model
1.  **Scores ($T$):** The coordinates of your samples in the new, reduced PLS space. If you plot the first two scores ($t_1$ vs $t_2$), you see how well the classes are separated.
2.  **Loadings ($P$):** These describe the relationship between the original features and the scores. They tell you the **direction** of a feature's contribution to an axis.
3.  **Weights ($W$):** The "bridge" between $X$ and $Y$. Weights represent the contribution of each feature to the maximization of covariance. Unlike loadings, weights are often unit-normalized to compare feature importance fairly.
4.  **Components ($H$):** The number of latent dimensions calculated. Usually, 2 or 3 components are sufficient for classification.

---

## 2. Feature Importance: The VIP Score

The **Variable Importance in Projection (VIP)** score is the gold standard for feature selection in PLS-DA. It summarizes how much a feature contributes to the model across all latent components.

### The Mathematics of VIP
For a feature $j$, the total VIP score is calculated as:
$$\text{VIP}_{j} = \sqrt{p \times \frac{\sum_{h=1}^H (s_h \times w_{hj}^2)}{\sum_{h=1}^H s_h}}$$

*   **$p$**: Total number of original features.
*   **$s_h$**: The **Sum of Squares** in the $Y$-space explained by component $h$. This represents the "significance" or "weight" of the component itself.
*   **$w_{hj}$**: The weight of feature $j$ on component $h$ (must be unit-normalized).
*   **$H$**: Total number of components.

### Component-wise VIP vs. Total VIP
You can calculate the VIP contribution of a **single component** ($i$):
$$\text{VIP}_{ij} = \sqrt{p \times \frac{s_i \times w_{ij}^2}{\text{Total } s}}$$

To get the **Total VIP**, you do not simply sum the component-wise VIPs. Instead, you follow the **Quadratic Rule**:
$$\text{Total VIP}_j = \sqrt{\sum_{i=1}^H \text{VIP}_{ij}^2}$$

### Why use $s$ instead of Loadings?
*   **Loadings ($P$)** tell you how a feature defines an axis. A feature could have a huge loading on Component 5, but if Component 5 doesn't help separate your classes, that feature is irrelevant.
*   **$s$ (Significance)** weights the features. It ensures that features defining "important" axes (those with high $s$) get higher VIP scores, while features defining "noisy" axes are penalized.

---

## 3. O-PLS-DA: Orthogonal PLS-DA

### The Motivation
In standard PLS-DA, the variance related to class separation (Predictive Variance) is mixed with variance that has nothing to do with classes (Orthogonal Variance, like batch effects or biological noise). This can make biplots difficult to interpret because the "class separation" axis might be tilted or spread across multiple components.

### The Mechanism
O-PLS-DA mathematically splits the $X$ matrix into two parts:
1.  **Predictive Component**: Variation correlated with $Y$.
2.  **Orthogonal Components**: Variation not correlated with $Y$.

### Benefits
*   **Interpretability**: Class separation is usually pushed entirely into the **first component**. This makes Biplots much cleaner, as you can see exactly which features drive the primary difference between Group A and Group B on a single horizontal axis.
*   **Interpretive Power**: It allows you to isolate and study "background noise" (the orthogonal part) separately from the classification signal.

---

## 4. sPLS-DA: Sparse PLS-DA

### The Motivation
Standard PLS-DA uses all $p$ features to build the model, giving every feature a non-zero weight. In datasets with thousands of features (e.g., genomics), this leads to "noisy" models that are hard to use for discovery.

### The Mechanism
sPLS-DA applies a **Lasso (L1) Penalty** to the weights ($W$) during the calculation of each component. This penalty "shrinks" the weights of unimportant features exactly to **zero**.

### Benefits
*   **Automatic Selection**: The algorithm identifies a "sparse" subset of features automatically.
*   **No Post-Hoc Filtering**: You don't need to calculate VIP scores and manually threshold them; the algorithm does the filtering during the training phase.
*   **Performance**: Often generalizes better on new data because it ignores noisy, low-impact features.

---

## 5. Comparative Summary

| Feature | **PLS-DA** (Standard) | **O-PLS-DA** (Orthogonal) | **sPLS-DA** (Sparse) |
| :--- | :--- | :--- | :--- |
| **Primary Goal** | Maximize $X-Y$ Covariance. | Separate Predictive from Noisy variance. | Feature selection via Sparsity. |
| **Handling Noise** | Mixes noise with signal. | Isolates noise into separate axes. | Ignores noise by zeroing weights. |
| **Selection Logic** | Post-hoc (Threshold VIP > 1.0). | Post-hoc (Loadings/VIP). | Built-in (L1-Penalty). |
| **Biplot Clarity** | Moderate (Diagonal separation). | High (Horizontal separation). | Moderate (Cleaner arrows). |
| **Best Case** | Small/Medium feature sets. | When interpretability is priority. | Very large feature sets (p >> n). |

---

## 6. Implementation Checklist
*   **Normalization**: Always normalize your weights ($w_{norm} = W / \|W\|$) before calculating VIPs to ensure components are comparable.
*   **Scaling**: PLS is sensitive to the scale of features. Always use **Standard Scaling** (Mean=0, Var=1) on $X$ before running the model.
*   **Cross-Validation**: Because PLS-DA is supervised, it is prone to overfitting. Always validate the number of components ($H$) using Q2 (predictive power) or Cross-Validation accuracy.
