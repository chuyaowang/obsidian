Here are comprehensive lecture notes based on the provided slides, structured into logical modules with transitionary text to ensure a smooth learning flow.

### **Lecture Topic: Low-Level Vision, Linear Filters, and Edge Detection**

**Overview:**

This lecture covers "Early Vision" (or Low-Level Vision), focusing on processing image data at the pixel level to extract meaningful primitive features. The progression moves from simple point operations (histograms) to grouping pixels (connected components), and finally to convolution-based operations for smoothing, edge detection, and feature matching.

---

### **I. Introduction to Low-Level Vision**

We begin by defining the scope of our subject. Low-level vision involves "bottom-up" processing. Unlike high-level vision, which uses top-down models to guide control (e.g., identifying "this is a cat"), low-level vision operates on generic prior knowledge without understanding the scene's semantic content.

* **Core Characteristic:** It is typically an image-to-image mapping. The input is an image, and the output is a processed image (e.g., edges, smoothed version, or a disparity map).
* **Common Operations:** These are functional operations recurring across different vision tasks, including histograms, thresholding, smoothing, edge detection, and resizing.
* **Style Transfer:** An exception to the rule. While traditionally low-level, modern "Image Style Transfer" maps the style of a reference image to an input image. However, performing transfer globally without semantic understanding can make the result look unrealistic.

*With a clear understanding that we are working with raw pixel data to create more "friendly" images, we turn to the simplest statistical tool available to us: the histogram.*

---

### **II. Histograms and Point Operations**

**1. Histograms**
A histogram is a simple counting of the occurrences of different gray levels in an image. It acts akin to a probability density function (PDF) for pixel intensities.

* **Applications:**
    * **Thresholding:** Determining a cutoff value to separate objects from the background.
    * **Features:** Used in classification or recognition to describe texture or color distribution.
* **High-Dimensional Histograms:**
    * **Color:** Three histograms (Red, Green, Blue).
    * **Gradients:** Histograms of edge directions (used in SIFT and HOG descriptors).
    * **Bag-of-Words:** Counts the frequency of image patches.

**2. The Checkerboard Shadow Illusion (Adelson's Illusion)**
The lecture uses a classic optical illusion to demonstrate that the human visual system does not act like a simple physical light meter.

* **The Phenomenon:** A light check in a shadow can reflect the same amount of light (luminance) as a dark check in bright light.
* **Mechanism:** The brain determines lightness based on **local contrast** (comparing a pixel to its neighbors) rather than absolute luminance. It also discounts gradual changes (soft edges) as shadows, while interpreting sharp edges as surface/paint changes.
* **Lesson for Computer Vision:** Simple pixel value analysis is often insufficient; context and local comparison matter.

**3. Thresholding**
This is the simplest form of segmentation for gray scale images.
* **Operation:** Set all pixels greater than a value $T$ to 1 (max) and all others to 0 (min).
* **Choosing $T$:** Ideally, the histogram is **bi-modal** (has two distinct peaks). The threshold $T$ is set in the "valley" between the two peaks. This can be generalized to local thresholds that adapt to local contrast.

*Once we have thresholded an image, we are left with a binary map of "on" and "off" pixels. To make this useful, we need to group these independent pixels into distinct objects using connectivity.*

---

### **III. Connected Components**

Connected Components Labeling produces a list of spatially connected, same-valued pixels. This is not a segmentation algorithm itself, but often a "clean-up" process after classification (e.g., detecting sky or grass regions).

**1. Connectivity Definitions**
* **4-Connectivity:** Two pixels are connected if they share an edge (up, down, left, right).
* **8-Connectivity:** Two pixels are connected if they share an edge *or* a corner (diagonals included).

**2. The Labeling Algorithm**
A recursive algorithm is intuitive (find a pixel, find its neighbor, recurse) but is problematic for large images as call stacks can go very deep. The standard efficient approach is a row-by-row algorithm:
1.  **First Pass:** Iterate through pixels. If a pixel is foreground:
    * Check neighbors (top and left).
    * If no neighbors are labeled, assign a new label.
    * If neighbors have different labels, note that these labels are "equivalent" (a label collision).
2.  **Resolve Equivalences:** Merge labels that were noted as equivalent so that connected regions share a single ID.
3.  **Second Pass:** Remap all pixels to their final, unique component label.

**3. Region Properties**
After labeling, we can calculate geometric properties for each object suitable for high-level vision:
* **Area:** The number of pixels.
* **Centroid:** Center of mass $( \bar{x}, \bar{y} )$.
* **Perimeter:** Count of boundary pixels.
* **Compactness & Aspect Ratio:** Used to filter out noise or specific shapes (e.g., removing "skinny" regions with high aspect ratios).

*Region analysis works well for binary shapes. However, real images have noise and complex gradients. To handle these continuous signals, we introduce the mathematical foundation of low-level vision: linear filtering.*

---

### **IV. Linear Filters and Convolution**

**1. Definition**
A linear filter creates a new image where each pixel is a weighted sum of the original pixel and its neighbors, using the same set of weights at each point.
* **Shift-Invariant:** If you shift the input image, the output shifts by the same amount.
* **Convolution:** The mathematical operation of applying this kernel (or mask) $H$ to image $F$. It is associative. The formula involves a summation over indices, typically represented as: $R_{ij} = \sum_{u,v} H_{uv} F_{i-u, j-v}$.

**2. Smoothing (Blurring)**
Smoothing is primarily used to suppress noise.
* **Box Filter (Averaging):** All weights are equal. This models a square aperture but isn't a good model for natural defocus and causes "ringing" artifacts.
* **Gaussian Filter:** The weights follow a bell curve (Gaussian distribution). This is isotropic (circularly symmetric) and provides a reasonable model for a fuzzy blob or defocused lens.
    * **Formula:** Proportional to $\exp\left(-\frac{x^{2}+y^{2}}{2\sigma^{2}}\right)$.
    * **The Role of Sigma ($\sigma$):** Controls the width of the kernel. As $\sigma$ increases, more neighbors are included in the average. This results in a blurrier image but suppresses noise more effectively.

**3. Noise Models**
* **Gaussian Noise:** The simplest noise model assumes independent, stationary, additive Gaussian noise.
* **Effect of Smoothing:** Because noise is usually independent from pixel to pixel, averaging neighbors tends to cancel the noise out (mean approaches zero), while the underlying signal (which changes slowly) is preserved. However, filtering independent noise results in correlated noise in the output.

*Smoothing prepares the image by removing noise, which is essential because the features we are looking for—edges—are defined by sharp changes, making them easily confused with noise.*

---

### **V. Edge Detection**

**1. The Logic of Edges**
An edge is a sharp change in image intensity. This can be caused by changes in reflectance, object depth (occlusion), or illumination (shadows).
* **Gradient:** To find changes, we compute the derivative. A strong derivative (gradient magnitude) indicates an edge.

**2. Derivative of Gaussian (DoG)**
We can approximate derivatives using **Finite Differences** (e.g., kernels like $[1, 0, -1]$).
* **Problem:** Finite difference filters respond very strongly to noise because noise looks like a high-frequency change.
* **Solution:** Smooth the image first to reduce noise, *then* differentiate.
* **Implementation:** Because convolution is associative, we do not need two steps. We can convolve the image directly with the **Derivative of the Gaussian** kernel.

**3. The Canny Edge Detector**
The standard for robust edge detection involves three major steps to clean up the "thick" edges produced by raw gradients:

* **Step 1: Non-Maximum Suppression (NMS):**
    The raw gradient gives wide responses. We want thin, 1-pixel edges.
    * *Algorithm:* Look along the direction of the gradient (normal to the edge). If the current pixel's magnitude is not larger than its interpolated neighbors ($p$ and $r$), suppress it.

* **Step 2: Linking and Hysteresis Thresholding:**
    Single thresholding breaks edges. Canny uses two thresholds: **High** and **Low**.
    * Start tracking edges at pixels above the **High** threshold (strong edges).
    * Continue tracking the edge as long as pixels remain above the **Low** threshold.
    * This ensures noise is ignored (below Low) but faint parts of strong edges are preserved (between Low and High).

*Edges help us find boundaries, but often we need to find specific patterns or textures. For this, we treat our filters not just as derivatives, but as templates.*

---

### **VI. Normalized Correlation and Pattern Matching**

**1. Filters as Templates**
We can view filters as **templates** or vectors. Applying a filter is mathematically equivalent to taking a dot product between the image patch and the filter vector.
* **Insight:** Filters respond most strongly to image patterns that "look like" the filter itself. For example, a derivative of Gaussian looks like an edge.

**2. The Problem with Standard Dot Product**
A simple dot product is sensitive to intensity (contrast) changes. A bright spot might yield a high response even if the pattern doesn't match perfectly.

**3. Normalized Correlation**
To make pattern matching robust to lighting, we use normalized correlation.
* **Concept:** Instead of just the dot product, we measure the **angle** between the image vector and the filter vector.
* **Calculation:** The filter output is divided by the root sum of squares (magnitude) of the values covered by the filter.

**4. Implementation Tricks**
* **Zero Response to Constant:** Ensure the filter sums to zero so it ignores constant background regions.
* **Subtract Mean:** Subtract the image average in the neighborhood when computing the normalizing constant.
* **Texture Matching:** Use absolute values to deal with contrast reversal (e.g., detecting a pattern regardless of whether it is white-on-black or black-on-white).

*While normalized correlation helps us match specific templates, sometimes we need to generically classify every window in an image to understand its structure—whether it is a flat area, an edge, or a corner.*

---

### **VII. Orientation and Window Representations**

This section details how to mathematically describe and classify different regions of an image (windows) based on how the pixels change.

**1. Laplacian of Gaussian (LoG)**
Instead of the first derivative (gradient), we can find edges using the second derivative.
* **Zero-Crossing:** An edge is located where the first derivative is maximum, which corresponds to where the second derivative crosses zero.
* **Logic:** The Laplacian is rotationally invariant. It is implemented by smoothing with a Gaussian and then applying the Laplacian, known as the LoG filter.

**2. Orientation Representation**
* **Why Orientation?** While gradient *magnitude* is affected by illumination changes, the *direction* (orientation) of the gradient is generally robust to lighting changes.
* **Describing Patches:** We can characterize an image patch by the "swing" (variance) of its gradient orientations.

**3. Classifying Window Types**
We can classify local windows based on the behavior of their gradients:
* **Constant Window:** Contains small gradient magnitudes (flat area).
* **Edge Window:** Contains a few large gradient magnitudes that are all in **one direction**.
* **Flow Window:** Contains *many* large gradient magnitudes, but still in **one direction**.
* **Corner Window:** Contains large gradient magnitudes that **swing** in different directions (significant change in $x$ and $y$).

**4. Representing Windows (The Structure Tensor)**
To formalize the window classification above, we calculate the second moment matrix, often called the **Structure Tensor ($H$)**.
* **Formula:** $H = \sum (\nabla I)(\nabla I)^{T}$.
* **Eigenvalue Analysis:** We analyze the eigenvalues ($\lambda_1, \lambda_2$) of the matrix $H$ to classify the region:
    * **Flat:** Both eigenvalues are small.
    * **Edge:** One large eigenvalue and one small eigenvalue (indicates change in only one direction).
    * **Corner:** Both eigenvalues are large (indicates change in all directions).

**5. Visualization**
These properties can be visualized by plotting ellipses for every window.
* **Size of Ellipse:** Represents the magnitude of the change.
* **Shape/Orientation:** Indicates the relation to edges (thin ellipse) or corners (round/large ellipse).