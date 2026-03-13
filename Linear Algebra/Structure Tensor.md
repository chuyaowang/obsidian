# The Structure Tensor in Image Processing

https://www.crisluengo.net/archives/1132/

## 1. What is a Structure Tensor?

The **Structure Tensor** (also known as the Second Moment Matrix) is a matrix derived from the gradient of a function. In image processing, it is a fundamental tool used to summarize the predominant direction and coherence of image gradients within a local neighborhood of a pixel.

Unlike the raw gradient vector $\nabla I = [I_x, I_y]^T$, which describes the direction of greatest change at a _single point_, the structure tensor aggregates gradient information over a _region_. This makes it robust to noise and capable of describing texture orientation and edge strength more reliably.

Mathematically, for an image $I(x, y)$, the structure tensor $S$ at a given pixel is a $2 \times 2$ symmetric positive semi-definite matrix defined as:

$$ S_w(p) = \sum_{q \in \text{window}} w(p-q) \begin{bmatrix} (I_x(q))^2 & I_x(q)I_y(q) \\ I_x(q)I_y(q) & (I_y(q))^2 \end{bmatrix} $$

Or, in continuous terms using convolution with a Gaussian window $G_\sigma$:

$$ S = G_\sigma * (\nabla I \nabla I^T) = \begin{bmatrix} G_\sigma * I_x^2 & G_\sigma * (I_x I_y) \\ G_\sigma * (I_x I_y) & G_\sigma * I_y^2 \end{bmatrix} $$

Where:

- $I_x$ and $I_y$ are the first-order partial derivatives (gradients) of the image.
- $G_\sigma$ is a smoothing kernel (typically Gaussian) that defines the "integration scale" or neighborhood size.
- $w(p-q)$ assigns a weight to the summation depending on how far is pixel $q$ from pixel $p$.

## 2. Interpretation and Eigenvalues

The structure tensor describes the local geometry of the image intensity. To understand the geometry, we analyze its **eigenvalues** ($\lambda_1, \lambda_2$) and **eigenvectors** ($\mathbf{e}_1, \mathbf{e}_2$).

Since $S$ is symmetric and positive semi-definite, its eigenvalues are real and non-negative. Let's assume $\lambda_1 \geq \lambda_2 \geq 0$.

- **$\mathbf{e}_1$ (Major Eigenvector):** Points in the direction of the greatest gradient energy (averaged over the window). This is the direction **perpendicular** to the dominant edge or flow.
- **$\mathbf{e}_2$ (Minor Eigenvector):** Points in the direction of the lowest gradient energy. This is the direction **parallel** to the dominant edge or flow (the orientation of the fiber or line).
- **$\lambda_1$ (Largest Eigenvalue):** Represents the strength of the average gradient in the direction of $\mathbf{e}_1$.
- **$\lambda_2$ (Smallest Eigenvalue):** Represents the strength of the gradient in the direction of $\mathbf{e}_2$.

### Geometric Cases:

1. **$\lambda_1 \approx \lambda_2 \approx 0$ (Flat Region):** There is no significant gradient in any direction. The region is homogeneous.
2. **$\lambda_1 \gg \lambda_2 \approx 0$ (Edge or Line):** There is strong variation in one direction ($\mathbf{e}_1$) and little variation in the orthogonal direction ($\mathbf{e}_2$). This indicates a strong linear structure (edge, line, fiber).
3. **$\lambda_1 \approx \lambda_2 \gg 0$ (Corner or Isotropic Texture):** There is strong variation in all directions. This indicates a corner or a complex texture pattern without a single dominant orientation.

## 3. Smoothing Angles: Why and How?

One of the most powerful applications of the structure tensor is smoothing orientation fields.

### The Problem with Vector Averaging

If you try to smooth the orientation of lines by averaging gradient vectors directly, you encounter the **cancellation problem**.

- A gradient vector pointing "up" is $(0, 1)$ (90°).
- A gradient vector pointing "down" is $(0, -1)$ (270° or -90°).
- Physically, both represent a vertical line. However, their vector average is $(0, 0)$. The orientation information is destroyed.

### The "Flip then Smooth" Approach (and why it fails)

A naive solution is to force all vectors into a 180-degree range (e.g., if $y < 0$, flip the vector).

- **The Flaw:** This creates a discontinuity (a "seam") at the boundary (e.g., the x-axis).
- If you have a vector at $179^\circ$ and one at $1^\circ$ (both horizontal), the "flip" logic might leave them as is. Averaging $179$ and $1$ gives $90^\circ$ (vertical), which is completely wrong.

### The Structure Tensor Solution

The structure tensor solves this by mapping the gradient vector $\mathbf{g}$ to a tensor $\mathbf{g}\mathbf{g}^T$. $$ \mathbf{g}\mathbf{g}^T = \begin{bmatrix} g_x^2 & g_x g_y \\ g_x g_y & g_y^2 \end{bmatrix} $$ Notice the terms are squared or cross-multiplied.

- Vector $(1, 1)$ results in $\begin{bmatrix} 1 & 1 \\ 1 & 1 \end{bmatrix}$.
- Opposing Vector $(-1, -1)$ results in $\begin{bmatrix} (-1)^2 & (-1)(-1) \\ (-1)(-1) & (-1)^2 \end{bmatrix} = \begin{bmatrix} 1 & 1 \\ 1 & 1 \end{bmatrix}$.

The tensors are **identical**. We can now smooth the components of the matrix ($J_{xx}, J_{xy}, J_{yy}$) using a Gaussian filter. The tensors reinforce each other rather than canceling.

### Recovering the Angle

After smoothing the tensor components to get $\bar{J}_{xx}, \bar{J}_{xy}, \bar{J}_{yy}$, we recover the orientation angle $\theta$ (of the structure, perpendicular to the gradient) using:

$$ \theta = \frac{1}{2} \arctan\left(\frac{2 \bar{J}_{xy}}{\bar{J}_{yy} - \bar{J}_{xx}}\right) $$

This formula is derived from diagonalizing the $2 \times 2$ matrix. The factor of $\frac{1}{2}$ maps the full $360^\circ$ circle of the $\arctan$ function back to the $180^\circ$ range of orientations, ensuring a continuous, seamless representation.

## 4. Applications in Image Processing

1. **Coherence Enhancing Diffusion:** Smoothing images along edges rather than across them to preserve structures while removing noise.
2. **Corner Detection:** The Harris Corner Detector is based on the eigenvalues of the structure tensor.
3. **Optical Flow:** The Lucas-Kanade method uses the structure tensor to solve for motion vectors.
4. **Fingerprint Analysis:** Estimating the local orientation of ridges.

---

## Summary Comparison

|Feature|Structure Tensor|Hessian Matrix|
|:--|:--|:--|
|**Order**|First-order derivatives ($I_x, I_y$)|Second-order derivatives ($I_{xx}, I_{xy}, I_{yy}$)|
|**Input**|Gradient Vector|Intensity Surface|
|**Measures**|Orientation, Edge Strength, Coherence|Curvature, Convexity, Shape|
|**Primary Use**|Edge orientation, Corner detection (Harris), Optical Flow|Blob detection (SURF), Ridge/Vessel detection (Frangi)|
|**Smoothing**|Essential (integration window)|Implicit (usually computed at specific scales $\sigma$)|