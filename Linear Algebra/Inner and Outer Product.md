# Inner and outer product

In mathematics, the inner product and the outer product are two different operations that can be performed on vectors. The inner product takes two vectors and returns a scalar, while the outer product takes two vectors and returns a matrix.

## Inner product

[How inner product came to be defined](https://few.vu.nl/~molenaar/courses/Math/chapters/07_orthogonality.html#independence-norm-and-orthogonality)

The inner product of two vectors is defined as the dot product of the vectors. $$X\cdot Y=X^TY=\|X\|\|Y\|\cos(\theta)$$, where $\theta$ is the angle between $X$ and $Y$.

Also calculated by summing the element-wise multiplication of $X$ and $Y$

A vector dot itself gives the square of the [Euclidean norm](Euclidean%20Norm.md) of the vector: $$X^TX=\|X\|^2$$

The inner product of two vectors is often used to measure the similarity between the vectors (cosine similarity).

## Outer product

The outer product of two vectors is defined as the tensor product of the vectors. The outer product of two vectors is often used to create a new vector that is perpendicular to both of the original vectors.
$$u\times v = uv^T$$,   where $u$ is represented as a $m \times 1$ column vector and $v$ is a $n\times 1$ column vector.

$uv^T$ is matrix multiplication

