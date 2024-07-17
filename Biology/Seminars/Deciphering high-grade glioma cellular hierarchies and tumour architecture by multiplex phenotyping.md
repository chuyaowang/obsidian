# Multiplex Phenotyping by Staining

> Akoya Biosciences
> Ludwig-Maximilians Universität München
> Alexander Beck
#seminar 

> [!info] Seminar Info
> High-grade gliomas are a group of malignant brain tumors with a dismal prognosis and exceptionally high intra- and intertumoral heterogeneity. Identifying complex phenotypes in these tissues enables us to better understand the cellular hierarchies and the overall tumor architecture.  
>   
> Leveraging novel multiplex phenotyping technologies coupled with advanced disease models based on human pluripotent stem cells (iPSC) and primary brain tumor cells can provide new insights into tumorigenesis, tumor evolution and targetable vulnerabilities within these tumors.  
>   
> This webcast will describe use of these advanced technologies and the resulting imaging data to build more representative preclinical models for rapid therapy identification and translation.

## Diffuse midline glioma (DMG)

- A brain tumor
- Caused by H3K27M mutation, identified by scRNA-seq
- Fast progression

## Research

- Multiplex staining of H&E, K27M, Ki67

## Multiplex phenotyping

- When to multiplex: 
	- see multiple markers (10, 15, 20 markers) in the same *cell* for complex phenotypes
	- need for spatial data analysis
	- scarce sample
	- in other cases, separate staining will suffice
- Picking the right multiplex marker: 
	- high expression in target population
	- very low expression in others
	- markers with sufficient antibody options
	- there is some limit on antibodies
- The structure ![](Pasted%20image%2020240426001908.png)
- Cycle: stain -> reveal -> remove; can be repeated for many cycles

## Image analysis

- MAV, Visopharm, QuPath (freeware)
- Segmentation on DAPI signal
- If possible, include non-nuclear markers in your panel, makes better images
- Have some redundancy for you populations
- Area analysis: measure the total area of your marker, like total red area, but this is not single cell analysis
	- Works great for vasculature
	- Where are the blood vessels, distance between, big or small, etc.

## Establish a robust ex vivo model of DMG

- Creating brain organoids ![](Pasted%20image%2020240426003629.png)
- Fusing DMG cells with the brain organoids
- Used H3K27M and other markers to evaluate fusion of DMG cells with brain organoids
- Assess markers change upon treatment
- The Akoya machine can simultaneously scan multiple organoids, very high throughput