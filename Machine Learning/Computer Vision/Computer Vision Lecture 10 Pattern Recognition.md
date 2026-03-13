# Pattern Recognition

## 1. Introduction: The Machine Learning Paradigm for Vision

**Context & Background:** Historically, Computer Vision (CV) relied heavily on hand-crafted rules and geometric models to understand images. However, the real world is messy—lighting changes, objects deform, and viewpoints shift. The modern approach relies on **Pattern Recognition and Machine Learning (ML)**. Instead of writing explicit rules for what a "chair" looks like, we show the computer thousands of examples and let it learn the underlying patterns.

**Core Concepts & Terminology:**

- **The Pipeline:** Sensing $\rightarrow$ Feature Extraction $\rightarrow$ Recognition/Classification $\rightarrow$ Class Output.
    
- **Feature Vector Representation:** An image or object is reduced to a vector $X = [x_1, x_2, ..., x_n]$. Each $x_i$ is a measurement or attribute. For example, in character recognition, a letter might be represented by the feature vector $X = [\text{area}, \text{height}, \text{width}, \text{number\_of\_holes}, \text{number\_of\_strokes}]$.
    
- **Classes and Classification:**
    
    - **Classes:** A set of $m$ known classes of objects. A class might have a known description (attributes) for each, or a set of training samples for each.
        
    - **Reject Class:** A generic class for objects that do not fit into any of the designated known classes.
        
    - **Classifier:** An algorithm or mathematical function that assigns an object to a specific class based on its extracted features.
        
- **Classification Paradigms (Old vs. New):** * _Classic Paradigm (Strict Pipeline):_ A strictly linear, one-way feed-forward process: Sensing $\rightarrow$ Feature Extraction $\rightarrow$ Recognition/Classification. The system relies purely on the isolated features extracted in that specific instance to make a decision.
    
    - _New Paradigm (Knowledge Integration):_ Introduces a **Knowledge Store** (containing rules, templates, and samples). The pipeline is no longer a one-way street; both the feature extraction and classification stages bi-directionally interact with this knowledge store. This allows the system to integrate additional context, top-down rules, or prior information to guide feature extraction and dynamically improve the final classification. _(Example: In Optical Character Recognition (OCR), a knowledge store might contain a language dictionary. If the classifier is unsure whether a blurry character is a '0' (zero) or an 'O' (letter), the knowledge store provides context. If the surrounding letters form the word "HELL_", the knowledge store feeds back the rule that an 'O' is highly probable, refining the feature extraction and correcting the classification.)_
        
    - _Zero-Shot Learning:_ A newer paradigm where the model recognizes objects it has never seen before by combining learned attributes (e.g., knowing what "green", "legs", and "head" look like to identify a frog without prior frog images).
        
- **Attribute Learning - A New Paradigm:** Moving beyond simple numerical features to learn human-understandable semantic attributes (e.g., "metallic", "round", "has legs"). In the context of pattern recognition, instead of directly recognizing the complex, holistic pattern of a specific class (like a "dog"), the system first recognizes mid-level semantic patterns (the attributes, like "has fur" or "has four legs"). These recognized attributes then act as a new, highly descriptive feature vector to make the final classification.
    
    - **Why use attributes?**
        
        - _Object description:_ Generating readable descriptions of objects rather than just numerical outputs.
            
        - _Targeted retrieval:_ Searching for items based on specific properties (e.g., "Find red, round objects").
            
        - _Zero-shot learning:_ Recognizing completely new classes without explicit training samples by using known attribute combinations.
            
        - _Object classification:_ Using attributes as an intermediate step to improve overall accuracy and robustness.
            
        - _Outlier discovery:_ Identifying anomalous objects that deviate from expected attribute patterns.
            
        - _Visual categorization:_ Organizing and grouping visual data based on shared, recognizable properties.
            

_Transition:_ Once we understand that we need to represent objects as vectors of numbers (features) and assign them to classes, the immediate question becomes: How do we build a classifier to make that decision?

## 2. Basic Discriminant Functions and Classifiers

**Context & Background:** A classifier is essentially a mathematical boundary drawn in our feature space. If a new feature vector lands on one side of the boundary, it's Class A; if it lands on the other, it's Class B.

**Core Classifiers Discussed:**

- **Decision Trees:** A sequence of simple, hierarchical questions. For character recognition, the root might ask "Number of holes?". If 0, go left; if 1, go right. It interleaves feature extraction with classification. _Pros:_ Easy to design, highly interpretable, and execution is fast.
    
- **Nearest Class Mean (NCM):** Computes the center (mean) of all training examples for a given class. A new point is assigned to the class with the closest mean.
    
    - _The Problem with NCM:_ It assumes classes form neat, spherical clusters. If a class is bimodal (has two distinct clusters) or elongated, NCM fails drastically.
        
- **Scaling Coordinates:** Euclidean distance between two feature vectors can be used to classify objects. For example, apple vs. pears using the distance between the vectors
    
    $$color, circularity$$
    
    , provided the features are numerical. However, Euclidean distance can be misleading if features are on different scales (e.g., weight in grams vs. height in kilometers). We divide the distance in each dimension by its standard deviation ($\sigma$). This transforms elliptical clusters into spherical ones, drastically improving distance-based classifiers.
    

_Transition:_ Simple distance metrics work in perfect scenarios, but real-world data is noisy and overlapping. To handle uncertainty, we must shift our perspective from pure geometry to probability.

## 3. Probabilistic and Bayesian Decision-Making

**Context & Background:** What happens when a bruised cherry and a good cherry look exactly the same under a specific lighting condition? Absolute certainty is impossible. Bayesian decision theory provides a framework to make the _most probable_ guess based on available evidence and prior knowledge.

**Core Concepts:**

- **Bayes' Rule:** $P(\omega_i | x) = \frac{p(x | \omega_i) P(\omega_i)}{p(x)}$
    
    - $P(\omega_i)$: **Prior probability** (How likely is this class before we even look at the image? e.g., bruised cherries are rare).
        
    - $p(x | \omega_i)$: **Likelihood** (Given that it _is_ a bruised cherry, how likely is this specific pixel intensity?).
        
    - $P(\omega_i | x)$: **Posterior probability** (The final decision: Given this pixel intensity, what is the probability it is bruised?).
        
- **Normal (Gaussian) Distributions:** Often, the likelihood $p(x | \omega_i)$ is modeled as a Gaussian curve characterized by a mean ($\mu$) and variance ($\sigma^2$). This allows us to mathematically represent the overlap between classes (e.g., the overlap in infrared reflectance between bruised and good cherries).
    

_Transition:_ We have assumed so far that our input "measurements" ($X$) are inherently good. But if we feed bad measurements into a great classifier, we get bad results ("garbage in, garbage out"). What makes a good feature?

## 4. The Art of Feature Extraction

**Context & Background:** Why can't we just use raw pixel values as our feature vector? As MIT's A. Torralba notes, pixels are highly sensitive. If you move a chair one inch to the left, every single pixel value changes, even though the object is the same. Features must capture the _essence_ of an object.

**Characteristics of Good Features:**

1. **Invariance:** Robust to changes in lighting, viewpoint, intra-class variation, rotation, scale, distortion, and occlusion.
    
2. **Discriminative Power:** Minimizes overlap between different classes.
    
3. **Low Redundancy:** Compact enough to be computationally efficient.
    

**Types of Features:**

- **Global & Block-Based Features:** Describe the entire image or broad regions within it.
    
    - _Tiny Images:_ A remarkably simple but effective global feature where the entire large image is drastically downsampled to a very low resolution (e.g., a 16x16 pixel tiny image). The feature vector is simply the flattened raw pixel values (e.g., $16 \times 16 \times 3 \text{ color channels} = 768$ dimensions). While it loses fine, local details, it preserves the coarse spatial layout and overall color distribution of the scene. Researchers at MIT (Torralba et al.) famously used 80 million tiny images paired with a simple K-Nearest Neighbors (KNN) search to perform successful scene classification.
        
    - _Color Histograms:_ Captures the distribution of colors in different channels (quantized into bins). It provides a good aggregate representation but inherently loses all spatial information. To make these features robust, they are often calculated in decorrelated color spaces (**LST** or **YCrCb**) rather than standard RGB to isolate pure color from illumination:
        
        - **LST (Luminance, S, T):** L represents intensity, while S and T represent chrominance (color). These components are mathematically transformed to be approximately decorrelated. A key advantage of LST is that the S and T components are intensity-invariant, and the S component specifically captures variations between daylight and tungsten lighting, making it excellent for indoor vs. outdoor scene classification.
            
        - **YCrCb (or YCbCr):** A popular transformation where Y is the intensity (brightness/luma) channel, and Cr and Cb are the red-difference and blue-difference color channels. Like LST, it completely isolates the grayscale intensity from the color information, allowing the classifier to handle shadows or lighting changes without misinterpreting them as different colors.
            
    - _Color Moments:_ An alternative to histograms that captures the statistical distribution of color across different channels. Instead of building bins, it computes statistical moments such as the **mean** ($m_1$, average color), **variance** ($m_2$ or $\sigma^2$, color spread), **skewness** ($m_3$, asymmetry of the color distribution), and **kurtosis** ($m_4$, sharpness of the distribution peak). The general formula for the $d$-th moment is $m_d = \frac{1}{n}\sum_{i=1}^{n}(x_i - \mu)^d$.
        
    - _Spatial Component of Color (Block-Based Features):_ Global color histograms and moments quantize data but keep _no spatial information_ (they don't know _where_ the red pixels are in the image, just that they exist). To fix this while keeping the representation compact, we can make the statistics local:
        
        - **Partitioning:** The image is divided into segments (e.g., a regular 10x10 grid) or regions grouped by clustering algorithms.
            
        - **Local Calculation:** Color features (histograms or moments) are estimated independently for each specific segment.
            
        - **Concatenation:** These regional features are concatenated sequentially to construct the final image feature vector. For example, if a 10x10 grid is used, and we compute 2 moments (mean and variance) across 3 color channels ($L^*u^*v^*$ or LST) for each block, the resulting feature vector has $100 \text{ blocks} \times 2 \text{ moments} \times 3 \text{ channels} = 600$ dimensions. This technique powerfully preserves the rough spatial layout of colors.
            
    - _Texture Features (Discrete Wavelet Transform - DWT):_ Images aren't just defined by color; texture is a highly discriminative property. DWT can extract these texture features by decomposing an image patch into different frequency "subbands" at various scales.
        
        - **Explanation of the slide statement:** _"The energy of a subband in a local neighborhood (excluding LL band) can be used as a texture feature. The texture feature vector is_ $x_t = [e_2, e_3, e_4, e_6, e_7, e_8]$_"_
            
            - **What this means:** When DWT is applied to an image block, it filters the image into a low-pass approximation (the **LL band**, which captures the overall smooth brightness/color) and several high-pass detail bands (like **HL, LH, HH**, which capture horizontal, vertical, and diagonal edges/textures).
                
            - Because the LL band just shows the blurred base image, we **exclude** it when looking specifically for _texture_. Instead, we calculate the **"energy"** ($e$) of the high-frequency subbands (usually the sum of the squared coefficients in that band).
                
            - If we perform a multi-level decomposition (e.g., a 2-level DWT), we get a set of detail subbands from the first level (let's say they are subbands 2, 3, and 4) and another set of finer detail subbands from the second level (subbands 6, 7, and 8).
                
            - By collecting the energy values ($e$) from these specific, high-frequency subbands, we construct a compact feature vector ($x_t$). This vector perfectly mathematically describes the roughness, directionality, and scale of the texture in that local neighborhood.
                
    - _GIST:_ Captures the spatial layout, texture, and overall "feel" of a scene without explicitly segmenting or recognizing individual objects. It summarizes the image by using a **steerable pyramid**. A "pyramid" means the image is analyzed at multiple scales (resolutions), while "steerable" refers to a bank of directional filters (like Gabor filters) that detect edges and gradients at various specific orientations (e.g., 0°, 45°, 90°). By pooling these responses across a grid, GIST creates a compact, low-dimensional signature of the scene (e.g., identifying a "tall building" scene vs. an "open country" scene based on the dominance of vertical vs. horizontal structural frequencies).
        
- **Local Features:** Describe specific patches or "interest points" of an image. Excellent for handling occlusion.
    
    - **SIFT (Scale-Invariant Feature Transform):** The gold standard of classical CV. It finds "keypoints" using Difference of Gaussians (DoG) across multiple scales, ensuring scale invariance. It then describes the patch around the keypoint using a 128-dimensional histogram of oriented gradients (HOG), ensuring rotation invariance.
        
    - **SURF (Speeded-Up Robust Features):** A faster version of SIFT. It achieves its speed primarily by utilizing **integral images**—a data structure where the value at any given pixel $(x,y)$ is the sum of all pixels above and to the left of it in the original image. Once an integral image is computed, the sum of pixel intensities within _any_ rectangular area can be calculated in constant time ($O(1)$) using just four array references. This makes approximating large filters (like the box filters used in SURF to approximate Gaussians) incredibly fast, regardless of the filter's size.
        
    - **HOG (Histogram of Oriented Gradients):** Excellent for pedestrian/silhouette detection. It provides a good representation of silhouettes and borders that is invariant to light contrast changes and small image movements. To calculate it, the image is partitioned into blocks (or patches), and the direction and magnitude of the gradient are calculated in each patch to build a histogram of these gradient orientations.
        
- **CNN Features:** In modern paradigms, we pass an image through a pre-trained Convolutional Neural Network (like AlexNet or VGG) and extract the activations from a fully connected layer (e.g., FC7) to use as a dense, highly semantic feature vector.
    

_Transition:_ When using local features like SIFT, an image is represented as a chaotic collection of hundreds of local descriptors. How do we feed a varying number of features into a classifier that expects a fixed-size vector?

## 5. Bag of Visual Words (BoW) & Search Strategies

**Context & Background:** The Bag of Visual Words model is directly borrowed from Natural Language Processing (NLP).

- **Bag of Words in NLP:** In text analysis, the Bag of Words (BoW) model is a way to represent a document. It completely ignores grammar, syntax, and word order. Instead, it simply defines a "dictionary" of known words and then counts the frequency of each word in a given document (creating a histogram). For example, a document containing the sentence _"it was the best of times, it was the worst of times"_ would be represented by the word counts: `{"it": 2, "was": 2, "the": 2, "times": 2, "best": 1, "of": 2, "worst": 1}`.
    
- **The Visual Analogy:** In Computer Vision, we treat an _image_ like a text document. Instead of text words, the image is made up of "visual words" (local image patches or features, like SIFT descriptors). Just as a language has a dictionary, we create a "visual vocabulary" by finding common visual patterns across all our training images. To represent a new image, we simply extract its patches, match them to the closest visual words in our dictionary, and build a histogram counting their frequencies.
    

**Core Concepts:**

- **Creating the Dictionary:** We extract millions of local features (like SIFT) from training images and cluster them (usually via K-Means). Each cluster center becomes a "visual word."
    
- **The BoW Histogram:** For a new image, we extract its features, match them to the nearest visual words in our dictionary, and build a histogram of word frequencies. This **fixed-length** histogram is our final feature vector.
    
- **Probabilistic Latent Semantic Analysis (pLSA):** Yet another powerful technique borrowed from NLP.
    
    - _In NLP:_ A document often isn't just a random bag of words; it contains underlying "topics." A news article might be a mixture of 60% "politics" and 40% "economics." pLSA is a statistical model that analyzes word co-occurrences to discover these hidden (latent) topics automatically.
        
    - _In Computer Vision:_ We apply pLSA to the Bag of Visual Words. Instead of mapping a raw histogram of visual words directly to an image class (like "farm"), pLSA introduces an intermediate layer of **latent visual topics** (e.g., 'sky patterns', 'grass textures', 'animal parts'). An image is thus modeled statistically as a _mixture_ of these latent topics. This provides a much richer, semantic representation of the image. It handles complex, cluttered scenes well because it can acknowledge that an image contains multiple different "topics" (e.g., a cow standing in a grassy field under a blue sky) rather than forcing it into one rigid, global histogram bucket.
        
- **Search Over Scale and Space:** To find objects (like faces) in an image, we use a "sliding window."
    
    - _Classical approach:_ Slide a box, shrink the image, slide again.
        
    - _Alternative:_ Keep the image the same size, but scale the feature-extraction window.
        

_Transition:_ Now that we have robust, fixed-length representations of our images, we can utilize more advanced, powerful classifiers to handle complex multi-class problems.

## 6. Advanced Discriminative Classifiers

**Context & Background:** Generative models (like Bayesian/Gaussian mixtures) model the underlying data distribution. Discriminative models, however, don't care about how the data was generated; they only care about drawing the absolute best line between the classes. They are highly accurate but computationally heavy during training.

**Core Classifiers:**

- **Support Vector Machines (SVM):** * _Concept:_ Finds the hyperplane that separates classes with the **maximum margin**. The training points closest to this boundary are called "Support Vectors."
    
    - _Soft Margin:_ Uses a "slack variable" to allow for some misclassification, preventing overfitting on noisy data.
        
    - _The Kernel Trick:_ When data isn't linearly separable (e.g., rings of data), a Kernel projects the data into a higher-dimensional space where a flat plane _can_ separate it.
        
- **Boosting (AdaBoost):**
    
    - _Concept:_ "Consult a team of weak classifiers." A weak classifier is just slightly better than random guessing.
        
    - _Mechanism:_ Train one weak classifier. See which data points it got wrong. Increase the "weight" (importance) of those hard points. Train the next classifier to focus on those hard points. Repeat. The final decision is a weighted vote.
        
    - _Viola-Jones Face Detector:_ Uses AdaBoost in a **Cascade Architecture**. Fast, simple features weed out 99% of background patches instantly, saving heavy computation only for face-like regions.
        
- **K-Nearest Neighbor (KNN):**
    
    - A purely data-driven, non-parametric approach. Plot the query image in feature space, find the 'K' closest training images, and take a majority vote.
        
    - _Example:_ Geotagging images by finding the visual nearest neighbors from a database of 1 million Flickr photos.
        

_Transition:_ A classifier is only as good as our proof that it works. We need rigorous metrics and testing protocols to ensure our models aren't just memorizing the training data.

## 7. Performance Evaluation & Validation

**Context & Background:** Simply stating "My model is 95% accurate" is dangerous. If a dataset has 99 non-faces and 1 face, a model that simply outputs "Not a Face" every time is 99% accurate, but completely useless.

**Core Metrics:**

- **Confusion Matrix:** A table showing True Class vs. Predicted Class. The diagonal represents correct predictions. It quickly reveals if a model frequently confuses "water" with "sky", or "4"s with "9"s.
    
- **Two-Class Metrics:**
    
    - _True Positives (TP), False Positives (FP), False Negatives (FN), True Negatives (TN)._
        
    - **Precision:** TP / (TP + FP) - "Of everything I called a face, how many were actually faces?"
        
    - **Recall (Detection Rate):** TP / (TP + FN) - "Of all the true faces out there, how many did I find?"
        
    - **ROC Curve (Receiver Operating Characteristic):** Plots the True Positive Rate against the False Positive Rate. The area under this curve (AUC) defines the robustness of the classifier.
        

**Cross-Validation:**

- **K-Fold Cross-Validation:** We must never test on the data we trained on (this leads to _overfitting_). We split the dataset into $K$ chunks (folds). We train on $K-1$ chunks and test on the remaining 1. We repeat this $K$ times, rotating the test chunk, and average the errors.
    
- _Stratified CV:_ Ensures each fold has roughly the same ratio of class labels.
    

## 8. The Importance of Datasets

**Context & Background:** Algorithms are only half the battle in Machine Learning; the other half is data. Datasets define the scope of the problem, allow benchmarking across the academic community, and provide the raw material for learning.

**Notable Vision Datasets:**

- _Early/Specific tasks:_ CMU PIE & FERET (Face recognition under controlled lighting/pose), Labeled Faces in the Wild (Unconstrained face recognition).
    
- _Segmentation & Scenes:_ LabelMe (Polygon outlines drawn by humans), 15 Scene Database, SUN (Large scale scene categorization).
    
- _Object Recognition Milestones:_ PASCAL VOC (Early standard for object detection), Caltech 256.
    
- _Video Tasks:_ TrecVid (Surveillance, news retrieval), UCF50/101 (Realistic action recognition from YouTube).
    
- **The Big Leaps:** * **ImageNet:** Over 14 million images categorized according to the WordNet hierarchy. This massive dataset directly fueled the Deep Learning revolution (CNNs).
    
    - **MS COCO:** Microsoft's dataset focusing on objects in context, pushing the field toward dense scene understanding and multiple-object segmentation.
        

_End of Lecture Notes. Keep these principles in mind when designing your own Computer Vision pipelines: Select robust features, pick the right classifier for the complexity of your data, and always validate rigorously!_