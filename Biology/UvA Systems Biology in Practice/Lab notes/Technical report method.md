
# Introduction

## Regulation of cyanobacteria growth by light and phosphate

![[Media/UvA SBiP Lab 2 2025-04-09 13.27.44.excalidraw]]

Both phosphate and light are key regulators for the growth rate of cyanobacteria. At the core, they are both connected to ATP synthesis. As more ATP is made, the cell has more energy for growth. Cyanobacteria takes in phosphate from the environment via its phosphate transporter, and the phosphate molecules are subsequently used in the synthesis of AMP, ADP, and ATP. Interestingly, ATP also powers the phosphate transporter that takes in phosphate molecules, forming a positive feedback loop. On the other hand, cyanobacteria are photosynthetic organisms. They can absorb light through chloroplasts and convert it into ATP. Light, extracellular and intracellular phosphate, and the metabolic need of the bacterial cell together form an intricate relation that regulates the growth of cyanobacteria.

## Method

### Study design

To study the effect of light (L) and phosphate (P) limitation to cyanobacteria growth and ploidy, we culture two groups of four _Synechocystis_ PCC6803 strains in which one group is light limited but not phosphate limited, and the other is phosphate limited but not light limited.

| Multi-cultivator | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   |
| ---------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| Strain           | WT  | WT  | WT  | WT  | WT  | WT  | WT  | WT  |
| Limitation       | P   | P   | P   | P   | L   | L   | L   | L   |

### Turbidostat

The turbidostat is a microbiology lab instrument that keeps the "turbidity", dictated by the cell density, approximately constant. It constantly monitors the optical density (OD) in the culture and adjusts it as needed by adding culture medium or removing cell culture when the OD exceeds a certain threshold. Keeping the cell density constant ensures the light limiting and phosphate limiting experiments are conducted across consistent environment conditions in which growth is not deterred or promoted by the number of cells present. Furthermore, from the OD measurements of the turbidostat, the growth rate of the cyanobacteria can be calculated.

### Multi-cultivator

In this experiment, four light limited and four phosphate limited wild type cyanobacteria strains were cultivated in a multi-cultivator. Besides acting as a turbidostat that monitors and keeps the OD constant across the 8 test tubes, the multi-cultivator also adjusts the phosphate availability to the bacteria and has a LED light that can be scheduled to brighten or dim to control the light condition. The multi-cultivator is controlled by custom software and enables efficient parallel cultivation of multiple samples for this study.

### Spectrophotometer

The spectrophotometer emits a beam of light containing chosen wavelengths on one side of the cuvette and measures the amount of light transmitted to the other side. In this experiment, the spectrophotometer measures the absorbance of 4 wavelengths at 634, 685, 720, and 730 nm. The 634 and 685 nm wavelengths are absorbed by two pigments of cyanobacteria, which reflect the pigment composition. The pigment composition is designed to be a sanity check that should differ in different light conditions. The 720 nm and 730 nm wavelengths are used to estimate cell numbers. These wavelengths were chosen since they were not absorbed by the aforementioned pigments.

### CASY Counter

In a CASY counter, cells are suspended in a buffer and pass through two measuring electrodes. The buffer creates an electric field that is disturbed by cells. By measuring the amount of disturbance, the quantity and size of the cells can be determined with high accuracy and precision for calculating the ploidy of the bacteria.

### qPCR

Quantitative PCR (qPCR) incorporates a fluorescent probe into the normal PCR process. As the DNA is expanded, the fluorescent signal is detected in real time. The $Ct$ value is the number of PCR cycles for the fluorescent signal to exceed a certain threshold. The more DNA at the beginning, the smaller the $Ct$ value. Hence, qPCR can be used for detecting DNA copy numbers. In this experiment, qPCR is used to determine ploidy in combination with the cell number data from the CASY counter.