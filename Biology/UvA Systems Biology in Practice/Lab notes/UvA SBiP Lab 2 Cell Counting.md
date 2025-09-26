# Lab 2

Apr-9-2025
[0. UvA SBiP](Biology/UvA%20Systems%20Biology%20in%20Practice/0.%20UvA%20SBiP.md)

## CASY counter

[CASY Counter](Biology/UvA%20Systems%20Biology%20in%20Practice/CASY%20Counter.md)
- Sample: the smaller sample taken from [UvA SBiP Lab 1 Cell Culture Collection](Biology/UvA%20Systems%20Biology%20in%20Practice/Lab%20notes/UvA%20SBiP%20Lab%201%20Cell%20Culture%20Collection.md)
- Buffer: a phosphate buffer providing the electric field
- Purge: refers to cleaning the system thoroughly with blank buffer. Removes remaining cell sample from last operation. An automatic operation.
- 1st run:
	- 10 $\mu L$ sample in 10 $mL$ phosphate buffer
	- Result: 4500 units
- 2nd run:
	- 5 $\mu L$ sample in 10 $mL$ phosphate buffer
	- Result: 2200 units
- 3rd run:
	- blank (did not run purge before 3rd run)
	- Result: 1100 units, less than 100 units expected
- Experiment handling:
	- The bacteria condenses at the bottom of Eppendorf tube easily. Before taking sample, shake the tube gently to make the concentration even.
	- Avoid bubble formation in all steps; bubbles interfere with CASY counter operation
		- When taking buffer from container, push the handle slowly and let the droplets slide down the wall to avoid bubble formation.
		- After pipetting sample into buffer. Gently use the pipet to draw up and release the fluid to mix the sample into the buffer. Then cap and shake the tube gently to make mixing more even.
		- When the counter draws fluid up, observe the channel through the viewing window, and no big bubbles should be observed.
- Observed bimodal distribution of cell size: some cells stopped growing in the fridge, leading to a peak corresponding to smaller sizes.

## Regulation of bacteria growth by phosphate and light

> Charlie asked a question. Filipe gave an elaborate answer.
> Extra information but Filipe recommended to add to final report

### The question

- Ploidy can be affected by phosphate levels and by growth. More phosphate also leads to more growth.
	- Confounder effect in _causality_ analysis
- How to condition on growth (hold growth constant) and study the effect of intracellular phosphate on ploidy?
- This can be done under **low light conditions**

### Regulation mechanisms

![[Media/UvA SBiP Lab 2 2025-04-09 13.27.44.excalidraw]]

- **Intracellular phosphate** comes from **extracellular phosphate** that is taken inside the cell via the **phosphate transporter**.
	- The phosphate transporter is an enzyme ([Enzyme type: transporter proteins](Biology/VU%20Basic%20Models%20of%20Biological%20Networks/5.%20VU%20BMBN%20Monomeric%20Enzyme%20Kinetics.md#Transporter%20proteins)) that uses **ATP**.
	- Intra and extra cellular **phosphate levels** affect the amount of **transporter** proteins made. When there is less need for phosphate, fewer **transporter** proteins are expressed.
	- Intracellular phosphate level affects **bacteria [Ploidy](Biology/UvA%20Systems%20Biology%20in%20Practice/1.%20UvA%20SBiP%20Introduction.md#Ploidy)** and **growth**
- **Intracellular phosphate** level determines how many **ATP** is made since ATP synthesis requires phosphate.
- **ATP** then powers the **phosphate transporter**.
	- Low phosphate $\rightarrow$ low ATP $\rightarrow$ low transporter $\rightarrow$ lower phosphate
	- vice versa
- Besides **phosphate**, ATP level is also regulated by **redox balance**
	- ATP is made by electron transport chain (**ETC**) and **glycolysis**
		- The ETC is a part of photosynthesis (oxidative phosphorylation). During ETC, $O_{2}$ is reduced into $H_{2}O$.
	- Both ETC and glycolysis contains redox balance
	- Redox balance refers to the balance between $NADH$ vs. $NAD^+$ and $FAD$ vs. $FADH$ vs. $FADH_{2}$. Containing $H$ means it is reduced.
		- In the ETC, $NADH$ and $FADH_{2}$ donate electrons and create a proton gradient. The proton gradient provides energy for ATP synthase to make **ATP**.
		- In glycolysis, a $NAD-NADH$ balance is also maintained while producing **ATP**. (drawing in [Glycolysis flux relations](Biology/VU%20Basic%20Models%20of%20Biological%20Networks/workgroup/WG12%20Plasmodium%20falciparum%20metabolism.md#Flux%20relations))
	- When ETC and glycolysis are more efficient, the cost of making ATP is lower. 
- This summarizes how light and phosphate together regulate cell growth
- In an experiment, light level can be maintained to be just enough to enable growth. Then phosphate level can be adjusted, and the corresponding growth rates can be measured. This results in a region of linear growth where growth rate varies linearly with phosphate level. In this region, tuning growth rate is easy.
	- Related to this: design specification when [making a working model of the system](Biology/VU%20Basic%20Models%20of%20Biological%20Networks/10.%20VU%20BMBN%20A%20Self%20Regulating%20Metabolism%20Model.md#How%20to%20make%20a%20working%20model%20of%20the%20system). Cells balance resources between growth and metabolism. The model was made by setting enzyme levels to support minimum growth and maximum metabolism. Then model parameters that produce these enzyme levels were fitted.

### Extra: disruption of redox balance

- Redox balance is sensed and controlled by cells by controlling metabolism. Redox imbalance leads to lower or stopped **ATP** synthesis and **reactive oxygen species (ROS)**  production. 
- Imbalance means there is
	- accumulation of $NADH$: reactions that use $NAD^+$ cannot proceed, halting ATP production
	- depletion of $NADH/FADH_{2}$: ETC activity goes down, reducing ATP synthesis
	- excess $NADH/FADH_{2}$: electron leak from the ETC
	- insufficient oxygen as the terminal electron receptor in the ETC: electron leak 
	- leaked electrons react with $O_{2}$, leading to ROS formation
- Types of ROS:
	- Superoxide ($O_{2}^-$)
	- Hydrogen peroxide ($H_{2}O_{2}$)
	- Hydroxyl radicals ($OH$)
	- ROS damages DNA, protein, and lipid
- Causes of redox imbalance:
	- Metabolic stress: overactive glycolysis or TCA cycle, leading to excess production of $NADH$ and $FADH_{2}$.
	- Excessive light can lead to overactive ETC in cyanobacteria, causing electron leakage and ROS formation
	- Hypoxia: reduced oxygen availability
	- Mitochondria dysfunction (for most eukaryotes): dysfunctional ETC
	- Toxins