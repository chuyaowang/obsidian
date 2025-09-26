# Lab 3

Apr-16-2025
[0. UvA SBiP](Biology/UvA%20Systems%20Biology%20in%20Practice/0.%20UvA%20SBiP.md)

## Biphasic separation of molecular compounds

- General idea: let polar compounds dissolve in polar, let apolar dissolve in apolar

> **Introduction from lab manual:** A common theme in omics is sample disruption, and extraction and separation of molecules of interest. During the practical you will apply a slightly modified version of the protocol published by Matyash et al. (J Lipid Res. 2008 May; 49(5): 1137-1146.) for the extraction of lipids. Like other biphasic extraction protocols it extracts samples through the addition of a mix of polar and non-polar solvents in which the samples are agitated. Subsequently water is added to drive phase separation in a polar and non-polar solvent layer in which the molecules inside the sample separate based on their own preferred environment. This separates molecules broadly into polar (water soluble) and non-polar (lipophilic) species. While non-soluble materials are pelleted to the bottom following centrifugation. This broad separation allows for the more targeted analysis of the extracted molecules by subsequent mass spectrometric analysis.

> [!info]- Why water is needed to separate the phases
> Methanol and MTBE (methyl tert-butyl ether) do not separate on their own because they are **partially miscible**. This means they can dissolve in each other to some extent due to their chemical properties:
> 
> ---
> 
> ### Why Methanol and MTBE Don't Separate
> 
> 1. **Polarity Difference**:
>    - Methanol is a polar solvent, while MTBE is relatively apolar. However, MTBE has some polar characteristics due to the oxygen atom in its ether group.
>    - This partial polarity allows MTBE to dissolve in methanol to a certain degree, preventing phase separation.
> 
> 2. **Hydrogen Bonding**:
>    - Methanol can form hydrogen bonds with MTBE's oxygen atom, further enhancing their miscibility.
> 
> 3. **Density**:
>    - Both methanol and MTBE have similar densities (methanol: ~0.79 g/mL, MTBE: ~0.74 g/mL), which makes it difficult for them to separate into distinct layers based on density alone.
> 
> ---
> 
> ### Why Water Is Needed
> 
> Water is introduced to drive phase separation through the following mechanisms:
> 
> 1. **Immiscibility with MTBE**:
>    - Water is highly polar and immiscible with MTBE. When added, it forms a separate aqueous layer, forcing MTBE into a distinct organic phase.
> 
> 2. **Partitioning**:
>    - Water interacts strongly with methanol due to hydrogen bonding, pulling methanol into the aqueous phase. This leaves MTBE in the organic phase.
> 
> 3. **Density Difference**:
>    - Water has a much higher density (~1 g/mL) compared to methanol and MTBE, which helps create a clear separation between the aqueous and organic layers.
> 
> 4. **Chemical Environment**:
>    - The addition of water alters the solubility dynamics, encouraging polar molecules to dissolve in the aqueous phase and non-polar molecules to partition into the organic phase.
> 
> ---
> 
> ### Chemistry in Lipid Extraction
> 
> In lipid extraction protocols like the Matyash method, water is essential for separating polar and non-polar molecules:
> - **Polar molecules** (e.g., amino acids, carbohydrates) dissolve in the methanol-water phase.
> - **Non-polar molecules** (e.g., lipids) partition into the MTBE phase.
> 
> This biphasic system ensures efficient extraction and separation of molecules based on their chemical properties. 

## Steps

### Reagents

![[Media/UvA SBiP Lab 3 Sample Pre-processing for MS 2025-04-16 13.54.11.excalidraw]]

### Equipment

- **2 ml Eppendorf tubes**: 3 in total; 1 for sample, 1 for polar, 1 for apolar
- **Eppendorf Tube Rack, Falcon Tube Rack**: place Eppendorf tubes
- **Micropipettes and tips**: move reagents between tubes
- **Ice Bucket with Ice**: cool the reagents and the reactant to minimize metabolism in the sample
- **Micro Centrifuge**: separate the undissolvable from the dissolvable
- **Vortex**: mix the samples with the reagents

### Protocol

1) You will find your sample tubes on ice with your solvents. Your samples are chilled as are your solvents to keep slow down metabolism. Often samples are extracted on dry ice to keep them frozen until extraction, however this is not the case for the current practical.
2) Take 300 ul of cold methanol and add it to your samples.
3) Take 900 ul of cold methyl-tert-buthyl-ether (MTBE) and add it to your samples.
4) Now resuspend your pellet in the solvent by pipetting it up and down carefully and transfer it to a 2 ml Eppendorf tube.
5) Vortex the sample vigorously for 30 seconds.
6) Add 250 ul of water and vortex vigorously for 30 seconds again, put on ice and observe phase separation occur.
	1) More water may be needed if the sample is too dry. The sample itself will soak up some of the water before the molecules are dissolved in it. 
	2) This could be the reason if phase separation is not visible. Try adding more water and see if phase separation appears.
7) Vortex the sample vigorously for 1 minute and put into the micro-centrifuge and spin for 5 minutes and maximum speed. Take care to balance the weight in the centrifuge rotor.
	1) A tube of water can be used to balance the weights if only an odd number of tubes are available
8) Take the sample out of the centrifuge and put on ice, and label 2 eppendorf tubes per sample, denoting polar and apolar phase on the tube. 
9) Once you have decided which of the phases is the polar layer, transfer both layers for each sample into the premarked Eppendorf tubes.

> Top: apolar phase, green color (because the bacteria is green), look oily
> Bottom: polar phase: red and brown color, depending on how much water was added
> Residue: undissolvable

- After biphasic separation, a **rotary evaporator** will be used to remove the water, methanol, and MTBE from the polar and apolar samples. So the amount of solvent added will not affect the data collected, but it will make the evaporation take longer time (usually in 5-10 hours).
- After evaporation, the dried sample is re-suspended in proper reagent for subsequent LC-MS or GC-MS

## Questions

### Likely locations

- **Proteins**: they are aggregated due to interactions between the side chains. As a result, they are condensed in the _pellet_. However, individual amino acids are considered metabolites and can still dissolve in the polar or apolar phase.
	- If the solvent chloroform is used, proteins will still aggregate but will form a thin white interface layer between the polar and apolar layers. In this case the polar layer can be reached by piercing the pipette across the interface layer.
- **Sugars**: sugar and sugar metabolites are _polar_.
- **Lipids**: lipids are _apolar_. Short fatty acid chains can still enter the polar phase.

### Sources of variation when processing many samples for a large multi-omic study

- Skill of the lab technician: how well the molecules are extracted
- Temperature, depending on the time of the day and the geographical location
- Instrumental difference: 
	- batch variation causes by state of the instrument. i.e. when it just started and when it has warmed up
	- the instrument's accuracy can deviate over time
	- interference from previous samples analyzed that remain in the instrument

### How to correct for the variation

- Skill of the lab technician:
	- Use a robot to handle sample pre-processing
	- Multi-channel pipette that can operate on multiple samples at the same time
- Temperature:
	- Use AC to maintain a consistent temperature
	- Close the blinds in the lab to avoid direct sunlight on the instrument. This is especially important in summer.
- Instrumental difference
	- Batch variation: place _internal standard_  in sample or load _QC_ samples between every few samples (5-10). Many softwares can correct for batch variation using the assumption that the internal standard or QC samples should produce approximately the spectra whenever it is analyzed.
		- Internal standard could be ${}^{13}C$ or ${}^{15}N$ labeled compounds. Their quantity (peak area), retention time, and peak shape are all known and can be used for correction.
		- QC sample could be a mixture of all the samples being analyzed.
	- Deviating accuracy: calibrate the instrument every few months, especially after restarting the machine. The manufacturer usually have standards and protocols for calibration. Cleaning the sample inlet and the ionizer if they can be cleaned.
	- Previous samples: after finishing analyzing a group of samples (e.g. all control) and before proceeding to the next group (e.g. all disease), run a few blank (only solvent, no sample) samples (3 is enough) to clean up the system. Before starting the analysis sequence, run a few blank samples to let the machine warm up. After the analysis sequence, run a few blank samples to rinse the system.

