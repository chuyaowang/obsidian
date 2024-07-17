# Dynamic Time Warping

Dynamic time warping (DTW) is an algorithm to align two time series sequences. The idea is very similar to [Dynamic Programming for Sequence Alignment](2.%20MIT%20CompBio%20-%20Dynamic%20Programming.md#Dynamic%20Programming%20for%20Sequence%20Alignment), or the [Needleman-Wunsch algorithm](3.%20MIT%20CompBio%20-%20Hashing,%20Database%20Search,%20BLAST%20algorithm.md#Global%20Alignment%20(Review)), except one is applied to time series data, and the other is used for aligning two text sequences.

## How DTW works

### Distance Calculation

Given two sequences $A = [a_1, a_2, \ldots, a_n]$ and $B = [b_1, b_2, \ldots, b_m]$, DTW computes a cost matrix where each element $(i, j)$ represents the cost of aligning elements $a_i$ and $b_j$​. Typically, this cost is calculated using a distance metric like Euclidean distance: $D(i, j) = \text{dist}(a_i, b_j)$

In the paper [Gene2role a role-based gene embedding method for comparative analysis of signed gene regulatory networks](Gene2role%20a%20role-based%20gene%20embedding%20method%20for%20comparative%20analysis%20of%20signed%20gene%20regulatory%20networks.md), the [Exponential Based Euclidean Distance](Exponential%20Based%20Euclidean%20Distance.md) was used to account for the [Power Law](Power%20Law.md) distribution of [Node Degree](Node%20Degree.md)s. 

This distance is analogous to the costs assigned to gap, match, and mismatch for each base in DNA sequence alignment.

### Accumulate Cost Matrix 

An accumulated cost matrix $C$ is constructed to store the minimum cost to align the sequences up to each point. The element $C(i, j)$ represents the minimum cost to align the subsequences $A[1:i]$ and $B[1:j]$. It is computed using: $$C(i, j) = D(i, j) + \min(C(i-1, j), C(i, j-1), C(i-1, j-1))$$

Here, $C(0, 0)$ is initialized to $D(0, 0)$, and the borders are initialized with appropriate boundary conditions.

### Optimal Path

The goal is to find the optimal warping path that minimizes the total cost. This path starts from $C(n, m)$ and traces back to $C(0, 0)$, following the path of minimal cost transitions (diagonal, vertical, or horizontal).

## Optimizations

- **Sakoe-Chiba Band**: Restrict the warping path to a diagonal band to reduce computations.
- **FastDTW**: An approximate version of DTW that improves efficiency while maintaining accuracy.

## Applications

Dynamic Time Warping (DTW) should be used to align two sequences in situations where the timing of the sequences may vary and you need to measure similarity or match patterns despite these temporal differences. Here are specific scenarios where DTW is particularly useful:

1. **Speech Recognition**:
    
    - Aligning and comparing spoken words or phrases, where the speed of speech can vary between different speakers or even the same speaker at different times.
2. **Gesture Recognition**:
    
    - Comparing time series data from sensors capturing hand movements or body gestures, where the speed and style of gestures can differ.
3. **Time Series Analysis**:
    
    - Comparing and aligning financial data, such as stock prices, sales data, or other economic indicators, where events may not be synchronized but exhibit similar trends.
4. **Medical Data Analysis**:
    
    - Aligning physiological signals like ECG, EEG, or other biometric data, which can have temporal variations but need to be compared for diagnostic purposes.
5. **Pattern Recognition in Wearables**:
    
    - Analyzing and matching patterns from wearable devices, such as heart rate monitors or fitness trackers, where the activity patterns may not be perfectly synchronized.
6. **Handwriting and Signature Verification**:
    
    - Comparing dynamic signatures or handwriting samples, where the speed and pressure of writing can vary.
7. **Music and Audio Processing**:
    
    - Aligning and comparing audio signals, such as aligning two performances of the same piece of music that may have slight variations in tempo.

### Key Considerations for Using DTW

- **Variable Timing**: DTW is ideal when sequences have variations in speed or timing. For example, one sequence might be a faster or slower version of another.
- **Non-Linear Alignments**: When you need to allow non-linear alignments to find the best match between sequences.
- **Complex Temporal Patterns**: When the sequences have complex temporal patterns that simple linear alignment methods can't handle.
- **Different Lengths**: DTW can handle sequences of different lengths, making it versatile for many applications.

### When Not to Use DTW

- **Real-Time Applications**: Due to its computational complexity, DTW might not be suitable for real-time applications without optimizations.
- **Very Large Datasets**: The O(nm)O(nm)O(nm) time complexity can be prohibitive for very large datasets without approximations like FastDTW.
- **When Simple Metrics Suffice**: If sequences are already well-aligned or simple metrics like Euclidean distance are sufficient, DTW might be unnecessarily complex.