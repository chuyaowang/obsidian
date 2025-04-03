# Belousov Zhabotinsky Reaction

## Reactions

$$
\begin{aligned}
BrO_3^- + 2H^+ + Br^- &\rightleftharpoons HBrO_2 + HOBr \\

HBrO_2 + H^+ + Br^- &\rightleftharpoons 2HOBr \\

HOBr + H^+ + Br^- &\rightleftharpoons Br_2 + H_2O \\

BrO_3^- + HBrO_2 + H^+ &\rightleftharpoons 2BrO_2 + H_2O \\

BrO_2 + Ce^{3+} + H^+ &\rightleftharpoons HBrO_2 + Ce^{4+} \\

2HBrO_2 &\rightleftharpoons BrO_3^- + HOBr + H^+ \\

Br_2 + CH_2(COOH)_2 &\longrightarrow BrCH(COOH)_2 + Br^- + H^+ \\

6Ce^{4+} + CH_2(COOH)_2 +H_2O &\longrightarrow 6Ce^{3+} + HCOOH + 2CO_2 + 6H^+ \\

4Ce^{4+} + BrCH(COOH)_2 + 2H_2O &\longrightarrow 4Ce^{3+} + HCOOH + Br^- + 2CO_2 + 5H^+ \\

Br_2 + HCOOH &\longrightarrow 2Br^- + CO_2 + 2H^+
\end{aligned}
$$

## Simplification

- For modeling the set of equations can be simplified
- We assume that $BrO_3^-$, $HOBr$, $BrCH(COOH)_2$, $Ce^{3+}$, $H^+$, and $H_2O$ are **present in excess**, that is, their concentrations do not change significantly over the course of the experiment. 
- In contrasts, the concentrations of $HBrO_2$, $Br^-$, and $Ce^{4+}$ do change a significant amount, so their rate equations dominate the dynamics of the oscillation.

**Simplified equations**:
- The first part:$$
\begin{aligned}
BrO_3^- + Br^- &\xrightarrow{1} HBrO_2 + HOBr\\

HBrO_2 + Br^- &\xrightarrow{2} 2HOBr
\end{aligned}
$$

  

- The second part:$$
\begin{aligned}
BrO_3^- + HBrO_2 &\xrightarrow{3} 2HBrO_2 + 2Ce^{4+} \\

2HBrO_2 &\xrightarrow{4} BrO_3^- + HOBr \\

CH_2(COOH)_2 + Ce^{4+} &\xrightarrow{5} \frac{1}{2} fBr^-
\end{aligned}
$$
- $f$ is a coefficient here, representing the assumed constant concentrations of other reactants.
- The first path consumes $Br^-$, while the second produces it. When the concentration $[Br^-]$ is _high_, the **first** path dominates, while when the concentration is _low_, the **second** one does.

## Exercise

- Write the **mass action kinetics** equations and the **differential equations**.
- Only $HBrO_2$, $Br^-$, and $Ce^{4+}$ change concentration
- The reactions are _irreversible_: no $k^-$s

### Mass action kinetics


## Solving the differential equations

- See notebook of WG4
- Concentration of $HBrO_2$, $Br^-$, and $Ce^{4+}$ with respect to time can be obtained by solving **the system of differential equations** together.
	- Since the 3 concentrations change together, the differential equations must be solved together.
- The result should have an oscillating pattern.

## Diffusion

- Add a diffusion term to the differential equations
- Start with a grid with 2 dimensions. We are modeling diffusion in 2 dimensions.
- The diffusion term is calculated as the Laplacian of the grid.
- The update interval $h$ is equivalent to multiplying the Laplacian by a diffusion constant. This is because the update interval determines how often the diffusion effect changes the concentration. For a long interval like 100s, it means that diffusion affects the concentration every 100s, meaning the molecule is diffusing very slowly. For a short interval like 1s, diffusion affects the concentration every 1s, meaning the molecule is diffusing fast. Hence it is equivalent to the diffusion coefficient.

## Simplified diffusion

- Update concentrations using update rules and diffusion together
- Diffusion is modeled as a convolution here.
	- Takes the mean of a certain number of neighbors
	- If the kernel center has lower concentration, it increases after averaging - the surrounding diffuses to it
	- Else if the kernel center has higher concentration, it decreases after averaging - it diffuses to the surrounding
	- Having more neighbors means diffusing to a greater distance in each update -> higher diffusion constant
- Initialize concentrations to random positive values between 0 and 1. Otherwise the updates will be the same everywhere or have numerical overflow.