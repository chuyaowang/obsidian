# Frequency Domain Analysis of Fluctuations of mRNA and Protein Copy Numbers within a Cell Lineage: Theory and Experimental Validation

#paper #candida 
[link](https://journals.aps.org/prx/abstract/10.1103/PhysRevX.11.021032)
[Grima lab](https://grimagroup.bio.ed.ac.uk/)
[papers that cite](https://ui.adsabs.harvard.edu/abs/2021PhRvX..11b1032J/citations)

Below is a detailed summary of the paper’s key points, with an emphasis on how it builds a bridge between the noisy time‐domain behavior of gene expression and a frequency domain description that unearths the fingerprints of underlying cellular processes.

---

## 1. Motivation

The paper is driven by the challenge of interpreting long-term, single-cell lineage data on gene expression—a task that traditional models, which assume _non-growing_ cells, cannot address. In experiments (often using fluorescence microscopy in microfluidic “mother machine” setups), scientists record _time traces_ of mRNA or protein abundances over many generations. These traces show noisy yet oscillatory behavior, with clear periodic components tied to the _cell cycle_. The authors are motivated to develop a model that not only explains the stochastic fluctuations inherent to _gene expression_ (transcriptional and translational bursting, degradation) but also explicitly incorporates _cell cycle features_ such as _DNA replication_, _gene dosage compensation_, and (a)symmetric _partitioning_ at cell division. By moving into the frequency domain, the paper seeks to extract “fingerprints” in the power spectrum that quantitatively link these subcellular dynamics to observable phenomena.

> [!info]- Gene Dosage Compensation
>
> **Gene dosage compensation** is a biological mechanism that ensures that genes produce the correct amount of their products—like RNA or proteins—even when the number of gene copies changes.
> 
> For example, during the cell cycle, a gene might be duplicated when DNA replication occurs, increasing its copy number from one to two. Without dosage compensation, this could lead to overproduction of that gene’s product. To prevent this, cells often **adjust the rate of gene expression per copy**, so the overall output stays consistent. It’s like turning down the volume on each speaker when you double the number of speakers—so the room isn’t twice as loud.
> 
> This effect is especially important in maintaining balance during development or in diseases like cancer, where copy numbers can vary widely.

---

## 2. Research Question and Background Context

**Research Question:**

How can one quantitatively relate the frequency content (i.e., the power spectrum) of time-series data from single cells to the rich _underlying dynamics_ of gene expression and cell cycle progression? In other words, what are the signatures in the frequency domain that encode the contributions from _transcription, translation, degradation, bursting, cell cycle duration variability, gene replication, and molecule partitioning at division_?

**Background Information and Data Acquisition:**

- **Experimental Data:** The study builds on time-lapse fluorescence microscopy datasets from single bacterial cells (notably *Escherichia coli*). These experiments track fluorescently labeled proteins (and, in principle, mRNAs) over many cell cycles. High temporal resolution is achieved through microfluidic devices that “trap” individual cells and record their dynamics over upwards of 70 generations.
- **Traditional Models:** Earlier work modeled gene expression using two- or three-stage stochastic models that assumed a fixed (or effectively constant) cellular volume, incorporating dilution via an effective decay reaction. Such models missed key cell cycle–related _oscillations_ and noise induced by events like _replication_ and _unequal partitioning during division_.
- **Cell Cycle Dynamics:** A key element of the background is the modeling of cell cycle durations as an **Erlang distribution**. The cell cycle is subdivided into “effective stages” to capture variations in doubling times and the impact of replication timing.

> [!info]- Erlang Distribution
> The **Erlang distribution** is a probability distribution used to model the total time required for a sequence of *k* independent events to occur, where each event happens after an exponentially distributed waiting time. In simpler terms, it's the distribution of the sum of *k* exponential random variables with the same rate. It’s a special case of the gamma distribution and is often used to model processes that occur in stages—like the progression through phases of the cell cycle.
> 
> ### Why it's used in this paper
> 
> In the paper *“Frequency Domain Analysis of Fluctuations of mRNA and Protein Copy Numbers within a Cell Lineage”*, the authors use the Erlang distribution to model **cell cycle durations** because:
> 
> 1. **Biological realism**: Experimental data show that the time between cell divisions (doubling time) is variable but not purely random. The Erlang distribution captures this variability better than a single exponential distribution by allowing the cell cycle to be broken into multiple “effective stages,” each with its own exponentially distributed duration. This reflects the fact that the cell cycle is composed of multiple biochemical processes that must occur in sequence.
> 
> 2. **Control over variability**: The Erlang distribution has a tunable parameter (the number of stages, *N*) that controls the **coefficient of variation** (CV² = 1/N). This means the model can flexibly represent anything from highly variable to nearly deterministic cell cycles, depending on the biological system being studied.
> 
> 3. **Mathematical tractability**: Using the Erlang distribution allows the authors to derive **closed-form analytical expressions** for the autocorrelation function and power spectrum of gene expression fluctuations. These expressions are essential for translating noisy time-domain data into frequency-domain “fingerprints” that reveal the influence of cell cycle variability, gene replication, and partitioning at division.
> 
> 4. **Experimental agreement**: The authors show that fitting experimental distributions of doubling times (from *E. coli* and other organisms) to Erlang distributions yields good agreement, validating the choice of this model for capturing real biological timing.
> 
> So, in essence, the Erlang distribution serves as a biologically grounded and mathematically convenient way to model the stochastic timing of cell division, which is crucial for understanding how gene expression noise propagates across generations in single-cell lineages. Let me know if you'd like to see how this affects the shape of the power spectrum or the classification of oscillatory behaviors.

---

## 3. Theoretical Foundations and Relevant Theories

The paper interweaves several theoretical frameworks:

- **Stochastic Gene Expression:**  
  The authors start with the chemical master equation formalism. They account for bursty gene expression—a phenomenon where mRNA or protein synthesis occurs in sporadic, random _bursts_. The burst size may follow a _geometric or a deterministic (delta) distribution_. This framework explains why the number of gene products fluctuates stochastically over time.

> [!info]- Geometric and Delta Distributions
> 
> - **Geometric distribution**: This models the number of trials until the first success in a sequence of independent, identical trials. In gene expression, it's often used to describe *bursty* production, where each “burst” randomly produces multiple copies of a molecule. The probability drops off geometrically—meaning small bursts are common, large bursts are rare, but possible.
> 
> - **Delta distribution** (also called *deterministic* or *Dirac delta* in this context): This isn’t a distribution in the traditional probabilistic sense—it's a mathematical abstraction. When used to model something like burst size, it means the burst always produces the same fixed number of molecules—say, exactly one. There’s no variability; it's a sharp spike centered on one value.
> 
> So in short: *geometric = variable burst size; delta = fixed burst size*. This difference lets researchers study how randomness in production affects overall gene expression behavior.
> 
> The authors used **geometric** and **deterministic (delta)** distributions to model burst size because these two cases capture the biologically observed extremes of gene expression dynamics and allow for a unified, flexible mathematical framework.
> 
> Here’s why each was chosen:
> 
> ### 1. Geometric Distribution – for *bursty* gene expression
> - **Biological rationale**: Many genes exhibit *transcriptional* or *translational bursting*, where multiple mRNA or protein molecules are produced in rapid succession. This is often due to a gene switching into an active state and firing off transcripts before returning to inactivity.
> - **Mathematical convenience**: The geometric distribution is memoryless and has a simple generating function, which makes it analytically tractable. It’s widely used in stochastic gene expression models because it captures the variability in burst sizes with just one parameter—the mean burst size.
> - **Experimental support**: Numerous single-cell studies have shown that burst sizes often follow a geometric distribution, especially for mRNA production in bacteria and eukaryotes.
> 
> ### 2. Deterministic (Delta) Distribution – for *nonbursty* gene expression
> - **Biological rationale**: Some genes produce their products one molecule at a time, with little variability in burst size. This is modeled by a delta distribution (i.e., always producing exactly one molecule per event).
> - **Modeling purpose**: Including the delta distribution allows the authors to represent nonbursty expression as a limiting case within the same framework. It also helps isolate the effects of burstiness on the power spectrum and autocorrelation functions.
> 
> ### Why include both?
> By allowing the burst size to follow **either a geometric or a delta distribution**, the authors could:
> - **Span a wide range of biological scenarios**, from highly bursty to strictly regular expression.
> - **Analyze how burstiness affects the frequency content** of gene expression fluctuations—especially the shape and height of peaks in the power spectrum.
> - **Maintain analytical solvability**: Both distributions have well-defined generating functions, which are essential for deriving closed-form expressions for the autocorrelation and power spectrum.
> 
> In short, these choices weren’t arbitrary—they reflect real biological diversity and enable the authors to build a general, predictive model that connects time-domain noise to frequency-domain structure.

- **Cell Cycle Modeling:** 
  They model the cell cycle as a series of _effective stages_, each with _exponentially distributed_ transition times. This leads to the overall doubling time being Erlang distributed. Importantly, the model incorporates events such as instantaneous gene replication (with consequent changes in gene dosage) and the possibility of asymmetric molecule partitioning at cell division.

> [!info]- Why exponential distribution
> The authors modeled **cell cycle stage transition times as exponentially distributed** to achieve both **biological realism** and **mathematical tractability** in their framework. Here's why that choice makes sense:
> 
> ### 1. Capturing Cell Cycle Variability with the Erlang Distribution
> They divide the cell cycle into *N* effective stages, each with an exponentially distributed duration. When you sum *N* such stages, the total cell cycle duration follows an **Erlang distribution**—a flexible model that can match experimentally observed variability in doubling times.
> 
> - **Why exponential per stage?**  
>   Because the **sum of N exponential stages** gives an Erlang distribution, which has a tunable variance. This allows the model to represent anything from highly variable to nearly deterministic cell cycles by adjusting *N*.
> 
> - **Biological support:**  
>   Experimental data from various organisms (including *E. coli*, yeast, and mammalian cells) show that **cell cycle durations are not purely exponential**, but their distributions can be well-approximated by Erlang distributions. This supports the idea of modeling the cycle as a sequence of memoryless (exponential) transitions between substages.
> 
> ### 2. Mathematical Simplicity and Analytical Power
> Using exponential transitions per stage ensures that the overall system remains **Markovian**—meaning the future state depends only on the current state, not the full history. This is crucial for:
> 
> - **Deriving closed-form solutions** for the autocorrelation function and power spectrum.
> - **Applying matrix exponentials and eigenvalue decompositions**, which are only tractable when the system has memoryless transitions.
> 
> This structure allows the authors to analytically compute how fluctuations in gene expression propagate across generations and how they manifest in the **frequency domain**—revealing oscillatory signatures tied to the cell cycle.
> 
> ### 3. Modeling Biological Processes as Multi-Step Chains
> Biologically, many processes (like DNA replication, protein synthesis, or cell growth) involve **multiple sequential steps**, each with some randomness. Modeling each step as an exponential process is a reasonable abstraction that captures this chain-like behavior.
> 
> ---
> 
> So in short: **exponential transitions per stage** give the model the flexibility to match real cell cycle variability, while keeping the math elegant enough to extract deep insights—especially in the frequency domain, where the authors decode the hidden rhythms of gene expression.

- **Frequency Domain Analysis and Fourier Transforms:**  
  A central theory is that the power spectrum—the Fourier transform of the autocorrelation function—reveals underlying periodicities. By writing the autocorrelation function $R(t)$ (which captures how gene product numbers at one time correlate with those at a later time) and then applying the Fourier transform via the Wiener–Khinchin theorem, the authors convert time-series data into a frequency-domain representation $G(\omega)$. In this frequency domain, peaks (especially those centered at the cell cycle frequency and its harmonics) become clear indicators of the rhythmic cellular processes.

> [!info]- Autocorrelation function, Wiener-Khinchin theorem, and Fourier Transform
> ### 1. What Are Autocorrelation Functions?
> An **autocorrelation function (ACF)** measures how similar a signal is to a time-shifted version of itself. In practice, for a time-dependent signal $X(t)$, its autocorrelation function at a lag $\tau$ is defined by:
> $$
> R(\tau) = \langle X(t) \, X(t+\tau) \rangle,
> $$
> where the angle brackets denote a time (or ensemble) average. This function tells you, for each time lag, how much the value at one time predicts the value later on. In many biological signals—such as the fluctuating copy numbers of mRNA or proteins—the ACF reveals periodicities or characteristic time scales (for example, due to cell cycle events).
> 
> ### 2. How Are They Calculated?
> Practically, the ACF is calculated by:
> 1. Taking the product of the signal value at time $t$ and at time $t + \tau$.
> 2. Averaging this product over the entire duration or over many realizations of the process.
> Numerically, if you have a discrete time series $\{x_1, x_2, \dots, x_N\}$, one way to approximate the autocorrelation at lag $k$ is:
> $$
> R(k) = \frac{1}{N-k} \sum_{i=1}^{N-k} (x_i - \bar{x})(x_{i+k} - \bar{x}),
> $$
> where $\bar{x}$ is the mean of the series. In the paper you mentioned, the ACF is derived analytically based on the underlying master equations of gene expression dynamics, incorporating effects like transcriptional bursting, cell cycle stage transitions, and partitioning at cell division.
> 
> ### 3. Why Does It Make Sense to Use the Autocorrelation Function Here?
> In the context of the paper *“Frequency Domain Analysis of Fluctuations of mRNA and Protein Copy Numbers within a Cell Lineage: Theory and Experimental Validation”*, the autocorrelation function is key because:
> - **Temporal Correlations:** It captures how fluctuations at one time point relate to those at another. Since cell cycle processes and gene expression events leave imprints over time (for example, through oscillations due to cell division), the ACF quantifies these regularities.
> - **Foundation for Frequency Analysis:** The ACF is the starting point for computing the power spectrum via the Wiener–Khinchin theorem (discussed next). The power spectrum then reveals hidden rhythmic features and peaks corresponding to cellular subprocesses.
> 
> ### 4. What Is the Wiener–Khinchin Theorem?
> The **Wiener–Khinchin theorem** states that, for a wide-sense stationary random process, the power spectral density (PSD) is the Fourier transform of its autocorrelation function:
> $$
> S(f) = \int_{-\infty}^{\infty} R(\tau)\, e^{-i 2 \pi f \tau}\, d\tau.
> $$
> In essence, this means that the frequency content (how much power is present at each frequency) of a time series can be directly computed from its autocorrelation.
> 
> ### 5. What Does It Mean to Apply the Fourier Transform via the Wiener–Khinchin Theorem?
> Applying the Fourier transform via the Wiener–Khinchin theorem involves:
> - First, computing the autocorrelation function $R(\tau)$ of a signal (or obtaining it from an analytical expression based on the model).
> - Then, taking its Fourier transform to obtain the power spectrum $S(f)$.
> This approach transforms the time-domain data (which might look noisy and irregular) into a frequency-domain representation where peaks indicate dominant cyclic or periodic behavior.
> 
> ### 6. Why Does It Make Sense to Use the Wiener–Khinchin Theorem Here?
> Using the theorem in this context is beneficial because:
> - **Linking Time and Frequency Domains:** The paper aims to “unearth” the fingerprints of underlying cellular processes (such as cell division, gene replication, and transcriptional bursting) that manifest as oscillatory patterns. The theorem provides a mathematically rigorous way to go from time-correlated fluctuations (captured by the ACF) to a spectrum that shows how much each frequency contributes.
> - **Filtering Out Noise:** By working in the frequency domain, the authors can distinguish between high-frequency noise and low-frequency periodic signals that are the hallmarks of specific cellular subprocesses. This analysis can reveal peaks corresponding to events like cell cycle durations even when the time-series data appear very noisy.
> 
> ### 7. Why Do the Peaks in the Frequency Representation Represent Cellular Subprocesses?
> The idea is that many cellular processes happen at characteristic time scales. For instance:
> - **Cell Cycle Events:** Cell division or replication might occur with a regular periodicity, so fluctuations in the associated gene expression will have a peak at a frequency corresponding to the inverse of the cell cycle period.
> - **Transcriptional Bursting:** If mRNA or protein synthesis occurs in bursts, these bursts will introduce correlations in time that, when transformed into the frequency domain, show up as additional peaks or shoulders at specific frequencies.
> - **Feedback and Regulation:** Regulatory mechanisms that impose periodic constraints or delays can also give rise to peaks in the PSD.
> Thus, when the autocorrelation function is Fourier transformed (using the Wiener–Khinchin theorem), distinct peaks in the power spectrum emerge at frequencies that map to these cellular subprocesses. These peaks serve as “fingerprints,” revealing the time scales and strengths of underlying biochemical events.
> 
> ---
> 
> In summary:
> - **Autocorrelation functions** measure how a signal correlates with itself over time lags and are computed by averaging products of shifted versions of the signal.
> - The **Wiener–Khinchin theorem** tells us that the power spectrum (frequency representation) is the Fourier transform of the autocorrelation function.
> - Using these tools makes sense here because converting noisy time-domain data (which carries the imprint of various cellular processes) into frequency space can isolate underlying periodic behaviors.
> - The peaks in the resultant power spectrum correspond to the characteristic frequencies of cellular subprocesses (such as cell division or transcriptional bursts), thereby providing insights into how these processes shape gene expression fluctuations.

- **Eigenvalue Decomposition:**  
  The analytical derivation exploits the fact that matrices governing cell cycle transitions (and the synthesis–degradation dynamics) are “circular.” This property allows the explicit computation of eigenvalues, so that the autocorrelation function can be expressed as a linear combination of exponential functions—and correspondingly, the power spectrum as a sum of Lorentzian functions.

> [!info]- Circular matrices, eigen decompositions, and Lorentzian functions
> Below is a detailed explanation that ties together the concepts of circular (or circulant) matrices, their eigenvalue decompositions, and how these relate to the autocorrelation function and the power spectrum—whose features are ultimately expressed as sums of Lorentzian functions.
> 
> ---
> 
> ### 1. Circular (Circulant) Matrices
> 
> **Definition:**  
> A circular (or circulant) matrix is a special kind of square matrix where every row is a cyclic shift (rotation) of the row above it. For an $N \times N$ circulant matrix, if the first row is  
> $$
> [c_0,\, c_1,\, c_2,\, \dots,\, c_{N-1}],
> $$  
> then the $k$th row is  
> $$
> [c_{N-k},\, c_{N-k+1},\, \dots,\, c_{N-1},\, c_0,\, c_1,\, \dots,\, c_{N-k-1}].
> $$
> 
> They are mathematically appealing because their eigenvalues and eigenvectors can be computed explicitly using principles from Fourier analysis. In fact, the Discrete Fourier Transform (DFT) diagonalizes circulant matrices.
> 
> ---
> 
> ### 2. Why Are Matrices Governing Cell Cycle Transitions and Synthesis–Degradation Dynamics Circular?
> 
> **Cell Cycle Transitions:**  
> In the paper, the cell cycle is broken into $N$ effective stages. A cell moves “cyclically” through these stages. When you impose such cyclic boundary conditions—for example, by letting the cell transition from stage $N$ back to stage 1—the resulting transition matrix is circulant. Typically, this matrix has constant off-diagonal entries representing the stage-to-stage transition rate (say, $\lambda$ for each stage) and a wrap-around entry in the last row that connects back to the first stage.
> 
> **Synthesis–Degradation Dynamics:**  
> Similarly, when modeling the degradation or production over a cycle or when the system is “periodic” in some effective process (for instance, the resetting across cell generations), the governing matrices can inherit a circulant structure. The idea is that the same rules apply at every stage of the cycle; therefore, the mathematical description becomes cyclic.
> 
> **What Values Do They Contain?**  
> - For the cell cycle, the matrix might contain on its diagonal the negative rate (e.g., $-\lambda$) and on the off-diagonals (or just above the diagonal) the positive transition rate ($\lambda$), with the final entry in the last row “wrapping” around to the first column.
> - In synthesis–degradation dynamics, the entries involve the production rate (often from bursting events) and the degradation rate (typically a constant $\mu$). When these dynamics are mapped onto the cell cycle (or assumed to be modulated by the cycle), their periodic nature gives rise to matrices with similar cyclic (circular) properties.
> 
> ---
> 
> ### 3. Why Compute Eigenvalues for These Matrices?
> 
> **Analytical Diagonalization:**  
> Because circulant matrices are diagonalized by the Fourier matrix (i.e., their eigenvectors are known explicitly), one can write the matrix exponential—which governs the time evolution of the process—in terms of its eigenvalues. This greatly simplifies solving the linearized system.
> 
> **Decomposition of Dynamics:**  
> By knowing the eigenvalues, you can express solutions (like the autocorrelation function) as a linear combination of exponential functions. That is, if $\lambda_i$ are the eigenvalues, then the time evolution terms contain factors like $\exp(\lambda_i t)$.
> 
> ---
> 
> ### 4. Decomposition of the Autocorrelation Function
> 
> **From Matrix Exponential to Exponential Functions:**  
> When you express the solution (or the autocorrelation function) using the eigen-decomposition, the matrix exponential splits into a sum over the eigenmodes:
> $$
> R(t) = \sum_{i} A_i\, \exp(\lambda_i t),
> $$
> where the coefficients $A_i$ depend on initial conditions and the eigenvectors. Each term represents an exponential decay (or growth) component with a characteristic time scale dictated by $\lambda_i$.
> 
> **Why Is This Useful?**  
> This form is key because it allows the authors to connect the deterministic and stochastic aspects of the cell’s biochemical processes with measurable quantities like the power spectrum.
> 
> ---
> 
> ### 5. From Exponential Functions to a Sum of Lorentzian Functions in the Frequency Domain
> 
> **Wiener–Khinchin Theorem:**  
> According to the Wiener–Khinchin theorem, the power spectrum is the Fourier transform of the autocorrelation function. Now, the Fourier transform of a simple exponential decay, $\exp(-\alpha t)$ (assuming $t \ge 0$) produces a function with the form
> $$
> \mathcal{F}\{e^{-\alpha t}\} \propto \frac{1}{(\alpha)^2 + \omega^2}.
> $$
> This is the standard form of a **Lorentzian function**.
> 
> **Sum of Lorentzians:**  
> Since the autocorrelation function is expressed as a sum of exponentials, its Fourier transform—the power spectrum—becomes a sum of Lorentzian functions:
> $$
> S(\omega) = \sum_i \frac{A_i}{(\lambda_i)^2 + \omega^2},
> $$
> possibly with additional shifts or modifications if the exponentials are complex (yielding shifted Lorentzians). The peaks in these Lorentzian functions correspond to the resonant (characteristic) frequencies of the underlying biochemical subprocesses.
> 
> ---
> 
> ### 6. What Are Lorentzian Functions and Why Are They Used Here?
> 
> **Definition:**  
> A Lorentzian function is given by:
> $$
> L(\omega) = \frac{A}{(\omega - \omega_0)^2 + \gamma^2},
> $$
> where:
> - $A$ is the amplitude,
> - $\omega_0$ is the central frequency (resonance frequency),
> - $\gamma$ defines the half-width at half-maximum (i.e., determines the spread or damping).
> 
> **Relevance:**  
> - They naturally arise as the Fourier transform of an exponentially decaying process.
> - In this context, each Lorentzian represents a mode (or eigenmode) of the cyclic processes (e.g., cell cycle transitions, synthesis–degradation), and its parameters (position, height, width) encode information such as the timing, strength, and variability of those processes.
> - The sum of these Lorentzians thus captures how different cellular subprocesses contribute to the overall fluctuation spectrum observed in experimental data.
> 
> ---
> 
> ### Summary
> 
> - **Circular matrices** are matrices with rows that are cyclic permutations of one another. They naturally arise when modeling cyclic processes like cell cycle transitions.
> - In the paper’s model, matrices for cell cycle transitions and synthesis–degradation are circular because the processes repeat identically in each cycle.
> - The entries in these matrices are the rate constants (e.g., transition rate $\lambda$ for cell cycle stages, degradation rate $\mu$, etc.).
> - The eigenvalues of these circulant matrices are computed because their analytic form is known, and because they allow the system’s response (like the autocorrelation function) to be written as a sum of exponential functions.
> - Since the Fourier transform of an exponential decay is a Lorentzian, this decomposition means the power spectrum is expressed as a sum of Lorentzian functions.
> - **Lorentzian functions** are peak-shaped functions (with the form $1/((\omega-\omega_0)^2+\gamma^2)$) that describe the frequency content (resonances) of the decaying exponential components.
> - They are used here because they naturally represent the spectral signature of the underlying biochemical processes; the position, height, and width of each Lorentzian reflect key features (like the timing of cell division and the noise in gene expression) that the authors can compare with experimental data.
> 
> This elegant mathematical framework—moving from circular matrices to eigenvalue decompositions, then to exponential decompositions of the autocorrelation function, and finally obtaining a sum of Lorentzian functions in the power spectrum—provides a quantitative “fingerprint” of the various cellular subprocesses underlying gene expression fluctuations.

---

## 4. Methodology

**Model Construction:**  
The authors develop a detailed stochastic model that integrates:
- **Transcription and Translation:** Occurring in bursts, with the burst size following an arbitrary distribution.
- **Degradation:** Modeled as first-order kinetics.
- **Cell Cycle Stages:** The cell cycle is divided into $N$ effective stages with distinct transitions, reflecting cell cycle duration variability.
- **Replication and Dosage Compensation:** The model assumes instantaneous gene replication at a fixed stage; after replication, the burst production rate may change to account for gene dosage compensation.
- **Cell Division:** The molecule partitioning at division can be asymmetric, with probabilities that capture realistic biases observed in organisms.

**Analytical Derivation:**  
- They transform the master equation into a system of generating functions corresponding to each cell cycle stage.
- By taking derivatives of these generating functions, the authors obtain closed-form expressions for the factorial moments (zeroth, first, and second), which are then used to express the autocorrelation function $R(t)$ in matrix form.
- Using an expansion in terms of eigenvalues and eigenvectors, the autocorrelation is decomposed into sums of exponential functions.
- Finally, a Fourier transform is applied to $R(t)$ to yield the power spectrum $G(\omega)$ as a sum of Lorentzian shaped curves. Here, the position, height, and width of the peaks provide crucial clues about the underlying kinetics.

**Numerical Simulations and Validation:**  
- The analytical power spectra are compared with the numerical spectra computed via the Gillespie stochastic simulation algorithm. By applying the Wiener–Khinchin theorem to simulated time traces, the authors show that the analytical predictions are in perfect agreement with the numerical results.
- The model’s predictions are further confirmed using experimental single-cell data from *E. coli* under different growth conditions.
- Moreover, by matching the experimental and theoretical power spectra, the authors can infer temperature-dependent gene expression parameters without needing direct fluorescence-to-molecule number calibration.

---

## 5. Key Results

- **Spectrum Types:**  
  The analysis identifies four distinct spectral types:
  - **Type I:** Unimodal spectrum that decreases monotonically with a peak at zero frequency.
  - **Type II:** Bimodal with an off-zero peak that is lower than the zero-frequency peak.
  - **Type III:** Bimodal with an off-zero peak greater than one.
  - **Type IV:** Unimodal bell-shaped with an off-zero peak higher than one.
  
  The transition between these types reflects the robustness of oscillations in gene expression and the effects of cell cycle variability.

- **Decomposition into Eigenmodes:**  
  The power spectrum is shown to comprise contributions from two sets of eigenvalues (one mainly governing the off-zero peak and the other mainly controlling the zero peak and spectrum decay). This decomposition demonstrates that distinct cellular mechanisms (e.g., cell cycle transitions versus protein decay) add unique signatures in the frequency domain.

- **Parameter Inference:**  
  By directly matching the peaks in the analytical power spectrum with experimental data, the method provides a rapid and robust way to _infer gene expression kinetic parameters_ — such as burst production rates, degradation rates, and the effects of cell division — without extensive calibration.

- **Agreement with Simulations:**  
  The analytical expressions derived for both the autocorrelation function and the power spectrum coincide perfectly with results from stochastic simulations, which confirms the validity of the model across a broad range of parameter settings.

---

## 6. Implications and Clinical Relevance

**Broader Implications:**  
- The framework offers a powerful tool to analyze and interpret long-term single-cell time series. In the frequency domain, seemingly noisy and complex time traces resolve into distinct spectral peaks that directly reflect underlying subcellular mechanisms.
- This frequency-based “fingerprint” can be used to quickly explore large regions of parameter space, enabling researchers to deduce how intricacies in the cell cycle and gene regulation impact the fluctuations in gene expression.

**Clinical Problem Addressed:**  
- Although the demonstration is focused on bacterial cells, the underlying methodology is broadly applicable. Many clinical problems—such as cancer progression, stem cell differentiation, and other disorders related to aberrant gene expression fluctuations—stem from disturbances in cell cycle control and intracellular dynamics.
- By providing a way to infer kinetic parameters and identify irregularities in cyclic behavior, the method can aid in diagnosing (or even predicting) pathologies where dysregulation of gene expression and cell cycle events is fundamental. For example, in cancer, abnormal oscillatory patterns in the expression of oncogenes or tumor suppressors might be detected with such an analysis, thereby informing treatment strategies.

---

## 7. Frequency Domain: A Window into Time-Domain Behavior

The paper’s central innovation is its development and usage of the frequency domain to decode time-domain fluctuations:
- **From Time to Frequency:**  
  The inherent challenge in biological time traces is that noise and variability (from bursty gene expression, variable cell cycle lengths, and partitioning asymmetry) mask the regularity that is imposed by the cell cycle. By transforming the autocorrelation function into the frequency domain using Fourier analysis, the method “disentangles” these effects.
  
- **Interpreting the Spectrum:**  
  - **Peak Position:** The location of the off-zero peaks corresponds to the cell cycle frequency (or its harmonics), directly linking observable oscillations in gene product numbers to cell division events.
  - **Peak Height and Width:** These features encode the robustness of the cell cycle’s influence amid the background noise. A narrow, high off-zero peak suggests highly robust oscillatory behavior, whereas a broader or lower peak indicates higher variability.
  - **Parameter Sensitivity:** Changes in burstiness, degradation rates, and asymmetric partitioning contribute in predictable ways to the spectrum. Thus, the power spectrum serves as a fingerprint that reveals the balance between deterministic cell cycle events and stochastic fluctuations.

By working in the frequency domain, the authors have turned a seemingly intractable problem — connecting complex, fluctuating time series with underlying biochemical processes — into one where the signal (cell-cycle rhythm) can be quantitatively extracted, analyzed, and exploited for parameter inference.

---

## 8. Conclusion

In summary, the paper provides a robust theoretical framework that:
- **Bridges the time and frequency domains:** By deriving closed-form analytical expressions for the power spectrum, the approach connects noisy, stochastic gene expression data to the underlying kinetics of cellular processes.
- **Incorporates detailed cell cycle dynamics:** It extends previous models by explicitly accounting for replication, dosage compensation, and (a)symmetric partitioning—all critical in real cell lineage observations.
- **Enables rapid parameter inference:** Matching experimental spectra to the theoretical model allows for the estimation of otherwise hard-to-measure rate parameters.
- **Offers potential clinical applications:** Although demonstrated with bacterial data, the method could be adapted to better understand diseases characterized by dysfunctional gene expression and cell cycle regulation, such as cancer.

This frequency-domain perspective not only yields insights into the mechanics of gene expression over time but also opens up promising avenues for diagnostic applications in biomedical research and clinical settings.

---

There is much more to explore regarding how the detailed eigenmode decomposition or the impact of promoter switching further refines these predictions. For example, one might next consider how these methods could be extended to mammalian cell data or used to study the impact of specific genetic mutations on the dynamical structure of gene expression.


---

## Hypothetical Research Plan

Below is an extensive hypothetical experimental plan that integrates concepts from the paper  
"Frequency Domain Analysis of Fluctuations of mRNA and Protein Copy Numbers within a Cell Lineage: Theory and Experimental Validation"  
with other relevant literature on fluorescence microscopy and microbial interactions. The plan is carefully designed to investigate how a fungal invasion affects a bacterial colony over time. At the end, a brief validation of the plan’s practicality is provided.

---

### 1. Experimental Overview and Rationale

**Objective:**  
To investigate the impact of a fungal invasion on a bacterial colony, with a focus on how the external perturbation alters the dynamical behavior of bacterial gene expression (e.g., cell cycle timing, bursty production) and stress signaling as measured via fluorescence microscopy. Key to our approach is not only conventional time-domain analysis (cell segmentation, tracking, growth rate measurement, etc.) but also frequency­-domain analysis (autocorrelation functions, Fourier transforms, and power spectral analysis) which reveals hidden periodicities (“fingerprints”) of cellular subprocesses.

**Rationale:**  
– The referenced paper shows that the frequency content of protein or mRNA fluctuations can encode detailed information about intracellular processes (such as transcriptional bursting and cell-cycle events).  
– In the context of a fungal invasion, the hypothesis is that the stress and physical contact (or secreted fungal molecules) will alter the dynamics of the bacterial colony. These alterations may result in changes of the average cell cycle duration, changes in burst parameters (size and frequency), and could even induce additional oscillatory features (or damp variability) that are uncovered by frequency domain analysis.

---

### 2. Biological Materials

#### A. Bacterial Strain

- **Species:** *Escherichia coli* (e.g., strain K-12 MG1655)  
- **Genetic Modification:**  
  - **Reporter Gene 1 (Fluorescence):** Constitutively expressed Green Fluorescent Protein (GFP) for general cell visualization and tracking.  
  - **Reporter Gene 2 (Optional):** A second reporter (e.g., an mCherry-tag fused to a cell division protein such as FtsZ or to a stress-responsive promoter) may be used to specifically follow cell cycle progression or stress signaling dynamics.  
- **Purpose:** Tracking individual cells to extract intensity time traces that contain information about cell growth, division, and gene expression dynamics.

#### B. Fungal Strain

- **Species:** *Candida albicans*  
- **Fluorescent Labeling:**  
  - **Option 1:** Genetically engineered to constitutively express Red Fluorescent Protein (RFP).  
  - **Option 2:** Alternatively, cells can be stained with a fluorochrome that binds to fungal cell-wall components (e.g., Calcofluor White) to permit detection by fluorescence microscopy.
- **Purpose:** To visualize fungal morphology and invasion dynamics so that spatial and temporal correlations with bacterial responses can be established.

---

### 3. Grouping of Samples (Experimental and Controls)

At least **three major groups** should be established:

1. **Bacterial Control (BC):**  
   - *E. coli* colony grown alone under identical culture conditions.

2. **Fungal Invasion (FI):**  
   - *E. coli* colony initially grown under the same conditions with a fungal inoculum introduced at a defined time point.

3. **Fungal Control (FC):**  
   - Fungal cells alone cultured on the same substrate to help calibrate fungal fluorescence and to check for spectral bleed-through.

*Optional Additional Groups:*  
- **Physical Separation Control:** Bacteria and fungi grown in adjacent but physically separated micro-chambers (sharing medium but not direct contact) to tease apart effects due to secreted molecules versus direct contact.

---

### 4. Culture Conditions and Experimental Apparatus

#### A. Culture Conditions

- **Medium:**  
  A co-culture medium that supports growth of both *E. coli* and *C. albicans*. For instance, a modified LB medium supplemented with additional sugars or nutrients and buffered appropriately might be used. (Alternatively, use a dual-phase medium or a minimal medium optimized for both organisms.)
  
- **Temperature:**  
  A compromise temperature (e.g., 30–37 °C) is chosen. For example, 37 °C is ideal for *E. coli* while many Candida strains grow well at 30 °C. Preliminary tests can establish optimal conditions.

- **Aeration & pH:**  
  The setup should provide sufficient oxygenation (e.g., with continuous flow in microfluidic devices) and maintain a stable pH.

#### B. Microfluidic Device Setup

- **Device Type:**  
  A PDMS-based microfluidic chip (“mother machine” style) with linear narrow channels that trap single or small groups of *E. coli* cells.  
- **Fungal Invasion Integration:**  
  The device should have an inlet (or side-channel) permitting controlled injection of fungal inoculum. The design must allow the fungus to invade the bacterial region while still enabling high-resolution time-lapse imaging.
  
- **Flow Control:**  
  A constant perfusion system to supply fresh medium and to enable a stable environment over a 24-hour (or longer) period.

---

### 5. Molecular Labels and Reagents

#### A. Proteins Labeled

- **Bacteria:**  
  - **GFP reporter:** Visualizes whole cell volume and provides a readout of overall gene expression.  
  - **(Optional) FtsZ-mCherry or Stress Reporter:** To delineate cell division events or expression changes due to stress.

- **Fungi:**  
  - **RFP (if genetically encoded) or Stained Marker:** To delineate the fungal structure, hyphae, and invasion front.

#### B. Reagents

- **Media and Supplements:**  
  - LB or modified medium compatible with both organisms.  
  - Selective antibiotics as needed (for plasmid maintenance in *E. coli*).
- **Fluorochromes (if required):**  
  - Calcofluor White (if using fungal staining instead of genetic RFP).  
- **Flow and Sterility Reagents:**  
  - Sterile PBS, paraformaldehyde (if fixation is needed post-run for additional analysis), and anti-fade reagents to minimize photobleaching.
  
- **Imaging Consumables:**  
  - Glass-bottom dishes or microfluidic chips with optically clear PDMS bonded to cover glass.

---

### 6. Data Collection Procedure and Time Points

#### A. Imaging Equipment

- **Microscope:**  
  An inverted fluorescence microscope with time-lapse capabilities (confocal or epi-fluorescence) equipped with multiple excitation/emission filters (GFP, RFP) and an automated stage.
  
- **Environmental Chamber:**  
  Maintained at the set temperature, with regulation of humidity and CO₂ if needed.

#### B. Data Collection Schedule

- **Duration:**  
  Continuous imaging for at least 12–24 hours to capture multiple bacterial generations (and fungal invasion progress).
  
- **Acquisition Interval:**  
  Images acquired every 5 minutes to resolve rapid gene expression fluctuations, cell divisions, and invasion events.
  
- **Channels:**  
  - GFP channel: Capturing bacterial cells and intracellular reporter fluctuations.
  - RFP (or equivalent) channel: Capturing fungal morphology and invasion.

#### C. Experimental Timeline

1. **Time 0:**  
   - Seed *E. coli* cells in the microfluidic device.
   - Begin continuous time-lapse imaging for the bacterial control group.
   
2. **First 2 Hours:**  
   - Allow the bacteria to acclimate and establish baseline behavior.

3. **Time = ~2 Hours (Invasion Time Point):**  
   - For the FI group, inject a known concentration of *C. albicans* (spores/hyphal fragments) through the designated inlet.
   
4. **Post-Invasion:**  
   - Continue time-lapse imaging for an additional 10–22 hours.
   - For all groups, capture multi-channel images, recording both bacterial and fungal signals.

---

### 7. Data Pre-Processing

#### A. Image Processing/Segmentation

- **Drift Correction & Registration:**  
  Align all images to correct for stage drift and microfluidic movement.
  
- **Background Subtraction:**  
  Remove background fluorescence to isolate the signal.
  
- **Segmentation:**  
  - Use ImageJ/Fiji or CellProfiler to segment individual bacterial cells based on GFP intensity.  
  - Similarly, segment fungal structures (hyphae) from the RFP/stained channel.
  
- **Tracking:**  
  - Use automated tracking algorithms (e.g., TrackMate in Fiji) to build cell lineages over time.
  - Extract cell contours and record fluorescence intensity as a function of time.

#### B. Data Extraction

- **Time Series Generation:**  
  - For each bacterium, extract the time series of mean fluorescence intensity.  
  - Flag cell division events (using a sudden drop in fluorescence due to partitioning, or accompanying second-reporter data) and record the cell cycle events.
  
- **Spatial Annotation:**  
  - Map positions to identify “invasion front” bacteria (cells nearest the advancing fungal hyphae) versus interior cells.

---

### 8. Downstream Data Analysis

#### A. Time-Domain Analysis (Traditional)

- **Growth & Division Metrics:**  
  - Compute generation times, cell doubling rates, and overall cell counts across groups.  
  - Compare the frequency and morphology (size, shape) of bacteria in the control versus invasion groups.
  
- **Intensity and Variance Analysis:**  
  - Analyze average fluorescence intensity and variance per cell.
  - Examine stress response if using a stress-inducible promoter.
  
- **Spatial Analysis:**  
  - Correlate fungal proximity with changes in bacterial cell size, shape, or intensity.
  - Map invasion front dynamics versus colony interior.

#### B. Frequency-Domain Based Analysis

- **Autocorrelation Function Calculation:**  
  - For each bacterial fluorescence time series, compute the autocorrelation function (ACF) to capture self-similarity across time lags.
  
- **Application of the Wiener–Khinchin Theorem:**  
  - Apply the Fourier transform to the ACF to obtain the power spectrum of each cell’s fluorescence fluctuations.
  
- **Power Spectrum Analysis:**  
  - Identify peaks in the power spectrum. In previous work, peaks corresponding to the cell cycle frequency and transcriptional bursting have been observed.
  - Decompose the power spectrum into a sum of Lorentzian functions—each representing an underlying dynamical process (e.g., cell division, burst events, stress response oscillations).
  - Compare the frequency content (peak positions, heights, and widths) between the bacterial control and fungal-invaded groups.
  
- **Parameter Inference and Statistical Testing:**  
  - Use nonlinear fitting to extract key parameters (e.g., effective cell cycle frequency, burst rate, effective noise parameters) from the Lorentzian fits.
  - Perform appropriate statistical tests (e.g., ANOVA) to determine if and how these parameters differ between groups.
  
- **Correlation with Spatial Data:**  
  - For bacteria near the fungal front, test whether frequency-domain features (e.g., increased off-zero peaks or broader frequency distributions) are significantly different from bacteria in the colony interior.

#### C. Integration with Conventional Data

- **Lineage and Clustering Analysis:**  
  - Cluster bacterial cells based on their dynamic frequency “fingerprints” to see if invasion induces distinct subpopulations.
  
- **Visualization:**  
  - Generate heat maps showing the spatial distribution of extracted frequency parameters.
  - Create kymographs to visualize both spatial and frequency dynamics over time.

---

### 9. Potential Interpretation of the Results

Depending on our findings, possible interpretations include:

1. **Altered Cell Cycle Dynamics:**  
   - In the FI group, we might observe a shift in the dominant frequency peak corresponding to the bacterial cell cycle. For example, a reduced or broadened cell cycle peak might indicate a stress-induced slowing or increased variability in division rates.
   
2. **Increased Noise or Bursting:**  
   - An elevated secondary peak (or additional peaks) in the power spectrum in the FI group could indicate enhanced transcriptional bursting or stress-induced oscillatory gene expression. This might be due to fungal secretions that activate stress-response pathways.

3. **Spatial Heterogeneity:**  
   - Bacteria at the invasion front may exhibit distinct frequency signatures compared to interior cells, suggesting a localized response to fungal contact or secreted metabolites.

4. **Amplitude and Phase Shifts:**  
   - Changes in the phase or amplitude of oscillatory components (revealed by the Lorentzian fits) might provide insight into modifications of the underlying regulatory feedback loops (e.g., altered gene dosage compensation or changes in promoter switching dynamics).

Collectively, these results would advance our understanding of inter-kingdom interactions, revealing not only gross changes in bacterial growth but also subtle shifts in the dynamic “fingerprints” of cellular processes as a result of fungal invasion.

---

### 10. Validation of the Plan’s Validity and Practicalness

Before undertaking the experiment, we validate the plan based on several criteria:

- **Strain Availability and Genetic Tools:**  
  *E. coli* K-12 MG1655 and *Candida albicans* are widely used model organisms. Fluorescent markers (GFP/RFP) are well established, and many labs already have protocols for constructing such strains.  
- **Microfluidic and Microscopy Infrastructure:**  
  Microfluidic devices (“mother machine” design) and high-resolution time-lapse imaging setups are standard in many cutting-edge microbiology labs. The imaging frequency (every 5 minutes) and 24-hour runs are within typical experimental parameters.
  
- **Data Processing Pipelines:**  
  Software packages such as Fiji (ImageJ), CellProfiler, MATLAB, or Python-based libraries for segmentation, tracking, and Fourier analysis are well documented. Frequency domain analysis (autocorrelation, power spectrum via the Wiener–Khinchin theorem) has been performed in previous studies, indicating feasibility.
  
- **Interdisciplinary Integration:**  
  The plan combines traditional quantitative microbiology and state-of-the-art frequency domain analysis. This integration has precedent in recent publications and is both innovative and realistic.
  
- **Feasibility of Sample Grouping:**  
  The grouping into bacterial control, fungal invasion, and fungal control is straightforward, and sample replication (e.g., n ≥ 3 for each condition) can be achieved.
  
- **Interpretation and Statistical Analysis:**  
  Statistical tools and modeling strategies for spectral analysis are well understood and have been used to extract parameters such as cell cycle duration variability and burst size in previous publications.

Overall, the plan is valid and practical, assuming access to commercially available strains, microfluidic devices, and standard fluorescence microscopy equipment. With careful optimization of co-culture media and imaging conditions to support both organisms, the experiment should yield high-quality data suitable for both conventional and novel frequency‐domain analyses.

---

### 11. Final Summary

In summary, the proposed experimental plan is designed to:

- Use genetically engineered *E. coli* (with GFP and optionally mCherry-labeled division/stress markers) and *Candida albicans* (expressing RFP or stained with a fungal-specific fluorochrome)  
- Culture them in a microfluidic device under controlled conditions, with defined groups (bacterial control, fungal invasion, and fungal control)  
- Image the samples continuously for 12–24 hours at 5-minute intervals via fluorescence microscopy  
- Preprocess the data by image registration, background subtraction, segmentation, and cell tracking to generate time series of bacterial fluorescence  
- Conduct both conventional time-domain analyses (growth rates, morphological changes, spatial distribution) and frequency-domain analyses using autocorrelation functions and Fourier transforms (per the Wiener–Khinchin theorem) to extract power spectra, which can be decomposed into Lorentzian functions  
- Interpret differences in the frequency spectrum (e.g., shifts in cell cycle frequency, changes in burst dynamics, additional peaks) as indicators of how the fungal invasion perturbs bacterial physiology  
- Validate that the plan is feasible with standard lab equipment and analysis pipelines

The expected outcome is that the fungal invasion will perturb the regular oscillatory “fingerprint” of the bacterial gene expression dynamics. Such perturbations might manifest as altered cell cycle durations, increased expression noise, or the presence of new periodic components—all of which can be quantitatively extracted via the frequency domain approach.

This plan effectively brings together established microbiological techniques with advanced signal-analysis methods, providing a robust strategy to understand inter-kingdom interactions at both the cellular and molecular levels.