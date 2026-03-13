# Amsterdam Imaging Symposium

#seminar 

## Imaging in Astronomy: a biased guided tour

> Daniela Huppenkothen, UvA

observations of mostly light

Gaia: 1.7 billion stars

Vera C Rubin Observatory: images entire visible night sky every 2 days
- 40 billion sources

most sources are point sources:
- stars: one point
- star cluster
- galaxy
- artifact
- cosmic rays

different wavelengths: optical vs. x ray, gamma, infared, atomic hydrogen, etc. For studying different objects in the universe

serendipity plays crucial role

Hanny's voorverp

Radio telescopes: the five hundred meter aperture telescope
- radiowaves are long

Interferometry: use difference in arrival time at different locations
LOFAR: antennae and earth's movement: gives more points
LoTSS field: sky model subtraction

what to do with astronomical images: 

imaging protoplanetary disks

classifying astronomical objects
- hubble de vaucouleurs diagram
- [galaxy zoo](www.zooniverse.org)

image classification:
- machine learning
- as galaxy becomes further away, it looks more like a star
- challenges:
	- lots of sources
	- training data hard to obtain
	- account for biases
	- solution: pre-training on simulations and domain adaptation

imaging differencing with convnets:
	finding transients in optical surveys
	requires complex pipeline
	goal: predict difference image from reference using convnets
	current approach: encoder decoder

challenge: deblending
	probability cateloguing
	machine learning
	additional information (spectra)

challenge: identification of sources across different resolutions
 - atmosphere obstructs light
 - radius based algorihtm
 - probabilistic matching
 - machine learning

estimating galaxy spectra from images
- expensive to obtain spectra
- Rubin and the Roman Space Telescope will generate vast amounts of galaxy images
- goal: predict galaxy spectra from broadband imaging

other dimensions as images: representation learning
- time series data

imaging in x-rays: pile-up
- ML models to deal with pile up

helping out serendipity: searching for anomalies

foundational models:
- combine multi-modal datasets
- images, spectra, tabular data, time series, etc. provide complementary information




## When Resolution is not everything: imaging complex materials and devices

> Peter Kraus, ARCNL

2Dm material: currently in lab, will be mass produced in the future



## Imaging Tomorrow: How Technology is Refining Diagnosis and Therapy

> Martijn de Bruin, Amsterdam UMC
> bme-physic.nl

- medical imaging research

gustav strijkers: MRI group

CINE MRI: MRI movies

AI for accelerating low field MRI
low SNR
deep learning reconstruction model

patient care journey:
- 1st consult
- dx imaging technology
- biopsy
- biopsy analysis
- treatment
- treatment follow-up
- all in separated locations




## Live Microscopy: cracking the challenge to image biology unfolding in cells, tissues, and organoids

> Kristina Ganzinger, AMOLF, Amsterdam
> amolf.nl

fluorescence microscopy trade-off triangle: spatial resolution, temporal resolution, \[light dose, may kill sample; imaging depth; signal to noise; data volume/analysis\]

topics:
- improving temp in single molecule microscopy without sacrificing snr ratio, Ganzinger team
- imaging depth and handling data volume, Tom Shimizu 
- data analysis following organoid development, Sander Tans, Jeroen van Zon group

DNA-PAINT-SPT microscopy

robotic imaging of symbiotic networks across scales
- data stored at SURF
- analyzed on the fly on Snellius (super computer)

intestinal cell differentiation by whole-organoid cell tracking
challenges:
- manual tracking
	- large cell numbers
	- 3D structure
- automated tracking:
	- dense packing
	- poor z-resolution
	- rapid movement
	- Organoid tracker: deep learning based approach
- more fundamental challenge: assess the correctness of the prediction
	- manual check
	- keep the high confidence only
	- developed: link probability from fluorescent signal
	- min cost flow solver to find links that maximize total likelihood




## Practical imaging in archeology: examples from the 4D research lab

> Mason Scholte, UvA

archeology and imaging go hand in hand
archeology can be destructive

landscape imaging




