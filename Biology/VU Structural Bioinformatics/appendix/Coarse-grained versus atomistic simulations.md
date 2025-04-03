# Coarse-grained versus atomistic simulations: realistic interaction free energies for real proteins

#paper 
## Abstract

- Whether two proteins will interact under physiological conditions is dependent on _interaction free energy_
- Use coarse grained (CG) molecular dynamics simulations to simulate protein-protein interactions and estimate interaction free energy
- Calculated the **free energy barrier** with respect to the bounded state using both atomistic and CG simulations for two pairs of interacting proteins:
	- TCR-pMHC complex
	- MP1-p14 complex
- Similar in accuracy to atomistic simulation, but 500x faster
- Extensive sampling critical for accurate free energy barriers, only feasible for CG simulation.
- Biological relevance of CG simulation
	- likely mutations (according to [BLOSUM62 Matrix](Biology/Concepts/BLOSUM62%20Matrix.md)) causes minimal changes in free energy barrier, while unlikely ones increases the barrier and makes the barrier much higher
	- dominant role of interface core in protein interactions

> [!info]- What are interface cores
> ### What Are Interface Cores?
> 
> Interface cores are regions within protein-protein interaction interfaces that are deeply buried and play a critical role in stabilizing the interaction. These residues are typically _hydrophobic_ and _less exposed_ to solvent, making them essential for the binding affinity and specificity of the interaction. They are surrounded by the **interface rim**, which is more solvent-accessible and often contributes to interaction specificity rather than stability.
> 
> ### How Do They Identify Interface Cores?
> 
> The authors identify the interface core by analyzing the **solvent-accessible surface area (SASA)** of residues in both the monomeric (unbound) and dimeric (bound) forms of the protein. Here's the process they use:
> 
> 1. **SASA Calculation**:
>    - They calculate the SASA for each residue in the monomer and dimer forms.
>    - Residues with less than 7% of their side chain exposed to solvent in both forms are classified as **protein core** residues.
>    - Residues with more than 7% SASA in the monomer but less than 7% in the dimer are classified as **interface core** residues.
> 
> 1. **Interface Rim Identification**:
>    - Residues with more than 7% SASA in both forms but showing a significant SASA difference (≥1 Å²) between the monomer and dimer are classified as **interface rim** residues.
> 
> 1. **Outer Interface Rim**:
>    - Residues adjacent to the interface rim on the same monomer are categorized as the **outer interface rim**.
> 
> This classification helps distinguish the deeply buried residues (interface core) that are crucial for binding stability from the more exposed residues (interface rim) that contribute to interaction specificity.

## Introduction

- Determining protein-protein interaction (PPI):
	- experimental techniques
	- prediction from sequences
	- protein-protein docking
- Challenges:
	- accurate determination of **interaction strength**
	- incorporating **protein flexibility**
	- accounting for water and small solute **entropic effects**
- Molecular simulations: addresses these challenges
- Implicit water: simulate water as a dielectric constant that dampens the electrostatic interactions
- Explicit water: simulate water as molecules
- Coarse grained (CG) simulation: group small molecules into 'meta-particles'
- MARTINI force field: a force field used for CG simulation
	- does not account for structural rearrangements, such as changes in secondary structure, since individual residues are grouped into meta-particles
- What they did:
	- estimate the free energy barrier with respect to the bounded state (interaction happening)
	- contribution of surface residues is sensitive to amino acid involved
	- mutations at the interface core and are evolutionarily unlikely affect the interaction strength more

> [!info]- Why choose these 2 pairs of protein complexes
> The authors chose the **TCR–pMHC complex** and the **MP1–p14 scaffolding complex** as their test cases because these protein pairs have well-characterized structures and interaction properties that were previously studied using atomistic simulations. Their reasons for selecting these specific pairs include:
> 
> 1. **Known Experimental Data**:
>    - Both complexes have experimentally determined free energy barriers and equilibrium structures, which provide a reliable benchmark to compare the coarse-grained (CG) and atomistic simulation results.
> 
> 1. **Structural Features**:
>    - The TCR–pMHC complex is a larger and more complex system with 707 residues, involving a key immune recognition interaction.
>    - The MP1–p14 complex is smaller, with 240 residues, and features a large, shallow interface, providing diversity in interface characteristics.
> 
> 1. **Relevance of Previous Studies**:
>    - Both systems had been extensively studied using atomistic simulations in the past (e.g., by Cuendet and Michielin for TCR–pMHC and Cui et al. for MP1–p14), offering a basis for direct comparison with the results of CG simulations.
> 
> ### Are Two Pairs Too Few?
> While two protein pairs can provide initial insights, they are **insufficient to generalize** the findings to all protein-protein interactions. The authors acknowledge this limitation in their discussion, noting that a larger dataset would be needed to claim universal applicability of coarse-grained simulations. However, they justify their approach by emphasizing:
> - The significant computational cost of atomistic simulations, which limits the scope of the study.
> - The biological relevance of the results for the selected complexes, which serves as a proof of concept for the viability of CG simulations.
> 
> Ultimately, their goal was to demonstrate that CG simulations can provide results comparable to atomistic simulations in terms of free energy barriers, computational efficiency, and biological relevance, using these two test cases as a starting point. For broader validation, further studies involving more diverse complexes would be required.

> [!note]- What is the MARTINI force field
> ### What is a Force Field?
> In molecular simulations, a **force field** is a mathematical model used to describe the potential energy of a system of atoms or molecules. It defines how atoms interact with each other through bonded (e.g., covalent bonds, angles, torsions) and non-bonded (e.g., van der Waals forces, electrostatic interactions) interactions. The force field provides equations and parameters that allow simulations to predict molecular behavior, such as dynamics, stability, and interactions.
> 
> Force fields are essential for molecular dynamics (MD) simulations, where they calculate the forces acting on atoms and determine their movements over time. Examples of widely used force fields include CHARMM, AMBER, and GROMOS.
> 
> ---
> 
> ### What is the MARTINI Force Field?
> The **MARTINI force field** is a coarse-grained (CG) force field designed for molecular dynamics simulations of biomolecular systems. It simplifies molecular systems by grouping several atoms into larger "beads," reducing computational complexity while retaining essential chemical and physical properties.
> 
> Key features of the MARTINI force field:
> 1. **Coarse-Graining**: On average, four heavy atoms and their associated hydrogens are represented by a single interaction bead. This reduces the number of particles in the system, allowing for faster simulations.
> 2. **Interaction Types**: MARTINI defines four main bead types—polar, non-polar, apolar, and charged—with subtypes to capture specific chemical properties.
> 3. **Applications**: It is widely used for simulating lipids, proteins, nucleotides, and other biomolecules, particularly in membrane-protein systems.
> 4. **Efficiency**: By simplifying the system, MARTINI achieves significant computational speed-ups compared to atomistic simulations, making it ideal for large-scale or long-timescale studies.
> 
> The MARTINI force field has been extensively validated and is known for its balance between computational efficiency and accuracy in capturing biomolecular behavior. If you'd like to explore its applications or setup, let me know!

> [!info]- Constraint force profile and PMF
> Constraint force profiles describe the forces required to maintain a system under specific constraints during a simulation or experiment. These profiles are particularly useful in molecular dynamics or mechanical systems to understand how constraints affect the behavior of the system. Here's a breakdown:
> 
> 1. **Definition**:
>    - In molecular dynamics, constraint force profiles represent the forces applied to keep certain degrees of freedom fixed or to maintain specific distances, angles, or other geometric properties between atoms or molecules.
>    - In mechanical systems, they describe the forces exerted by constraints (e.g., joints, surfaces) to limit the motion of objects according to predefined rules.
> 
> 1. **Applications**:
>    - **Molecular Dynamics**: Used to calculate the potential of mean force (PMF) by constraining the system along a reaction coordinate and measuring the forces required to maintain those constraints.
>    - **Mechanical Systems**: Help analyze how constraints like hinges, sliders, or fixed points influence the motion and stability of a system.
> 
> 1. **Calculation**:
>    - Constraint forces are typically computed during simulations by applying algorithms like the Lagrange multiplier method or penalty-based methods. These ensure that the constraints are satisfied while calculating the forces acting on the system.
> 
> 1. **Example in Molecular Dynamics**:
>    - When studying protein-protein interactions, constraint force profiles can be used to measure the forces required to separate two interacting proteins along a specific pathway. This data is then integrated to derive the PMF, which provides insights into the interaction strength and energy barriers.
> 
> In this paper, **constraint force profiles** are used to calculate the **potential of mean force (PMF)**, which describes the interaction strength between two proteins. 
> 
> ### **How Constraint Force Profiles Are Used**
> 1. **Reaction Coordinate**:
>    - The **center of mass (COM) separation** between two interacting proteins is chosen as the reaction coordinate.
>    - Constraint force profiles are generated by applying constraints to maintain specific COM distances during simulations.
> 
> 1. **Force Calculation**:
>    - The **mean force (Fmean)** required to maintain the constraint at each distance is calculated. This includes contributions from direct interactions and solvent effects.
> 
> 1. **Integration to Obtain PMF**:
>    - The constraint force profile (Fmean as a function of distance) is integrated to derive the PMF. The PMF provides a free energy profile along the reaction coordinate.
> 
> 1. **Free Energy Barrier ($\Delta G_{\text{off}}$)**:
>    - The free energy barrier is extracted from the PMF as the difference between the minimum (bound state) and the maximum (unbound state) of the profile.
> 
> ### **Insights Gained**
> - The PMF derived from constraint force profiles allows the authors to compare the interaction strengths predicted by CG and atomistic simulations.
> - It demonstrates that CG simulations, despite their simplicity, can achieve similar accuracy to atomistic simulations while being computationally faster.
> 
> This approach highlights the utility of constraint force profiles in quantifying interaction strengths and validating the biological relevance of CG models.

## Methods

### Software

- DSSP, JOY: absolute and relative solvent accessibility
- GROMACS: molecular simulation
- Modeller script `mutate_model`: produce mutant structures
- MARTINI force field: all 20 amino acids were mapped into four different bead types with respect to their physicochemical properties

### The potential of mean force

- PMF is not exactly free energy as it does not account for dilution effects when pulling the protein apart. However, the correction is small and it can be treated as effectively free energy profiles.
- Reaction coordinate: center of mass separation
- Constraint force: the force required to maintain a distance for a certain center of mass separation ^0756de
- The constraint force is calculated at each separation distance in simulation, forming a profile of forces. Then the constraint force profile is integrated to calculate the potential of mean force
- Explained in equations below:
	- $F_{\text{mean}}$ calculated for each $r$, averaged over _time_ in an NPT ensemble; $F$ encompasses direct interaction forces and indirect effects through solvents; $\vec{r}_{u}$ is a unit vector connecting the 2 centers of masses.
		- $F_{mean}(r)=\frac{1}{2}\langle(\vec{F}_{B}-\vec{F}_{A})\cdot \vec{r}_{u}\rangle_{NPT}$
	- For each $r$, different but similar starting configurations are used, and $F_{\text{mean}}$ for each starting configuration are averaged together.
	- $r$ defined as distance between centers of masses; a range of discrete values of $r$ (around 50) were sampled at. 
		- $r=|r_{\text{COM,A}}-r_{\text{COM,B}}|$
	- $\text{PMF}$ is obtained by integrating the interpolated $F_{\text{mean}}$ curve; $r'$ is a dummy variable here
		- $\text{PMF}(r)=-\int_{0}^r F_{\text{mean}}(r') dr'$
	- Error of $F_{\text{mean}}$ is estimated as the standard deviation from the replicate simulations (using different starting configurations) at each distance $r$. The error of PMF is calculated as: $\sigma_{\text{PMF}}(r)=\sqrt{ \int_{r}^0\sigma^2_{F_{\text{mean}}}(r')dr' }$

> [!info]- Why integration of force gives energy
> Integrating over $F_{\text{mean}}$ gives the **free energy**, or the **Potential of Mean Force (PMF)**, because it is mathematically based on the relationship between force and energy in physics.
> 
> ### **Why This Works**
> 1. **Force and Energy Relationship**:
>    - In classical mechanics, force (\( F \)) is related to potential energy (\( G \)) through the equation:
>      $$
>      F = -\frac{dG}{dr}
>      $$
>      where \( r \) is the reaction coordinate (e.g., center-of-mass distance). This means the force is the negative gradient (or slope) of the potential energy with respect to distance.
> 
> 1. **Reversing the Equation**:
>    - Rearranging the equation, we see that the potential energy difference (\( \Delta G \)) between two points along the reaction coordinate can be obtained by integrating the force:
>      $$
>      \Delta G = - \int F \, dr
>      $$
>    - Here, $F_{\text{mean}}(r)$ is the mean force calculated at different distances $r$, and the integral sums these forces to compute the change in free energy.
> 
> 1. **Thermal and Solvent Effects**:
>    - Since the mean force ($F_{\text{mean}}$) is averaged in the isothermal-isobaric ensemble, it inherently accounts for thermal fluctuations and solvent-mediated interactions. This makes the resulting PMF a thermodynamic quantity describing the system's free energy landscape.
> 
> 1. **What the Integral Represents**:
>    - The integration effectively accumulates the work done in moving the system along the reaction coordinate $r$, yielding the free energy barrier, wells, or transitions between states (e.g., bound and unbound configurations).
> 
> ### **Context in the Paper**
> In this study:
> - $F_{\text{mean}}(r)$ is derived by constraining the system at specific distances ($r$) and averaging the forces required to maintain these distances.
> - By integrating $F_{\text{mean}}(r)$ over the reaction coordinate, the authors calculate the PMF, which provides the free energy profile of the interaction between the protein complexes. This profile reveals critical information, such as the strength of binding and the energy barriers to dissociation.
