# The Hessian Matrix in Computer Vision

https://www.crisluengo.net/archives/1132/

## 1. What is the Hessian Matrix?

While the [Structure Tensor](Linear%20Algebra/Structure%20Tensor.md) is based on _first-order_ derivatives (gradients), the **Hessian Matrix** is a square matrix of **second-order** partial derivatives of a scalar-valued function (the image intensity). It describes the local **curvature** or convexity of the image intensity surface.

For a 2D image $I(x, y)$, the Hessian matrix $H$ at pixel $(x, y)$ is:

$$ H(I) = \begin{bmatrix} \frac{\partial^2 I}{\partial x^2} & \frac{\partial^2 I}{\partial x \partial y} \\ \frac{\partial^2 I}{\partial y \partial x} & \frac{\partial^2 I}{\partial y^2} \end{bmatrix} = \begin{bmatrix} I_{xx} & I_{xy} \\ I_{yx} & I_{yy} \end{bmatrix} $$

Since the order of differentiation usually does not matter for smooth images ($I_{xy} = I_{yx}$), the Hessian is a symmetric matrix.

## 2. Interpretation and Eigenvalues

The Hessian describes how the gradient changes. Just like the Structure Tensor, we analyze the Hessian using its eigenvalues $\lambda_1$ and $\lambda_2$ (let $|\lambda_1| \geq |\lambda_2|$).

These eigenvalues represent the **principal curvatures** of the image intensity surface at that point.

- **$\lambda_1$:** The curvature in the direction of maximum curvature (second derivative).
- **$\lambda_2$:** The curvature in the orthogonal direction.

### Geometric Classification (Shape Index):

By looking at the signs and magnitudes of $\lambda_1$ and $\lambda_2$, we can classify the local shape:

1. **$\lambda_1, \lambda_2$ both negative:** The intensity surface is a local hill (maximum). This corresponds to a **bright blob** on a dark background.
2. **$\lambda_1, \lambda_2$ both positive:** The intensity surface is a local valley (minimum). This corresponds to a **dark blob** on a bright background.
3. **$\lambda_1$ large negative, $\lambda_2 \approx 0$:** The surface curves down in one direction but is flat in the other. This corresponds to a **bright ridge** or **tube** (like a blood vessel or actin fiber).
4. **$\lambda_1$ large positive, $\lambda_2 \approx 0$:** This corresponds to a **dark ridge** or valley.
5. **$\lambda_1, \lambda_2$ have opposite signs:** This is a **saddle point**.
6. **$\lambda_1 \approx \lambda_2 \approx 0$:** The region is flat (planar).

## 3. Applications in Computer Vision

### A. Blob Detection (SURF and DoH)

The **Determinant of the Hessian** (DoH) is a popular measure for blob detection. $$ \text{det}(H) = \lambda_1 \lambda_2 = I_{xx}I_{yy} - I_{xy}^2 $$

- If $\text{det}(H)$ is large and positive, both eigenvalues have the same sign, indicating a blob (peak or pit).
- The **SURF (Speeded Up Robust Features)** algorithm approximates the Hessian matrix using box filters to detect interest points very quickly.

### B. Vessel and Ridge Detection (Frangi Filter)

The **Frangi Vesselness Filter** is the standard method for detecting tubular structures (blood vessels, neurites, cytoskeletal fibers). It explicitly uses the eigenvalues of the Hessian.

For a bright tube on a dark background, we look for pixels where:

1. $|\lambda_1|$ is large (high curvature across the tube).
2. $|\lambda_2|$ is small (low curvature along the tube).
3. $\lambda_1 < 0$ (the curvature is convex/downward).

The filter combines these criteria into a probability-like measure: $$ V_0(s) = \begin{cases} 0 & \text{if } \lambda_2 > 0 \ \exp\left(-\frac{R_B^2}{2\beta^2}\right) (1 - \exp\left(-\frac{S^2}{2c^2}\right)) & \text{otherwise} \end{cases} $$ Where $R_B = |\lambda_1|/|\lambda_2|$ (Blobness ratio) and $S$ is the norm of the Hessian (structure strength).

### C. Keypoint Localization (SIFT)

While SIFT uses Difference of Gaussians (DoG) to find keypoints, it uses the Hessian to **filter out edge responses**. Edges are unstable keypoints. SIFT checks the ratio of eigenvalues (similar to the Harris corner response but using the Hessian) to ensure the detected point is a corner/blob and not just a point along an edge.