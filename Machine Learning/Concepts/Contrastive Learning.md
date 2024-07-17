# Contrastive Learning

[Understanding contrastive learning](https://towardsdatascience.com/understanding-contrastive-learning-d5b19fd96607)

## Definition

A self-supervised ML approach to learn the general features of a dataset without labels by teaching the model which data points are similar or different.

## How

[SimCLRv2](https://towardsdatascience.com/a-framework-for-contrastive-self-supervised-learning-and-designing-a-new-approach-3caab5d29619)

SimCLRv2 is a contrastive learning framework proposed by Google Brain.

SimCLRv2 is composed of 3 steps:
1. Data augmentation is performed on an image to generate a pair of augmented images.
2. The pair is each fed to a convolutional neural network to create vector representations. The model will be trained to output similar vectors for similar images.
3. The similarity of the two vector representations are maximized by minimizing a contrastive loss function.

The model will learn that the pair should have similar representations and different from other images.

### Data augmentation

Any combination of the following augmentations are applied randomly: crop, resize, color distortion, grayscale. This is done twice for each image to create one positive pair for each original image.

There are also negative pairs created by pairing the augmented images with other images in the batch.

### Encoding

The pair is fed to the CNN model to encode both of them as vectors. This can be described as $$h=f(x)$$.

The output of CNN is then inputted to a set of Dense layers called the projection head, $z=g(h)$ to transform the vectors into another space. This is done to improve performance.

By transforming the image into latent space representations, the model is learning the high-level features of the image.

P.S. for sequential data (text), recurrent neural networks (RNN) is used.

### Loss minimization of representations

Given two transformed vectors, we need to define a similarity function. A natural choice for vectors are the **cosine similarity**.

We also need a loss function to minimize. SimCLRv2 chose the NT-Xent (Normalized Temperature-Scaled Cross-Entropy Loss). See details in the original blog.

### Optimization

The model's weights are updated with optimization algorithms such as gradient descent.

## Supervised contrastive learning

There is also a supervised contrastive learning approach. Here, the labels are used to define similarity and dissimilarity.

The Information Noise Contrastive Estimation (InfoNCE) is used as the loss function.

## Applications

### Semi-supervised training

We want to be able to use both the labeled data _and the unlabeled data_ to optimize the performance and learning capacity of our model. This is the definition of **semi-supervised learning**.

Contrastive learning can be used to pre-train the CNN model such that given limited labels, it can perform classification better.

### NLP Analog

Similar approach is applied in NLP. In the word2vec algorithm, the model is trained to give words that are closer together similar vector representations. These representations can be used in downstream tasks such as text classification.


