---
title: Mass Accuracy and Isotope Ratio Deviation
theme: solarized
---

# Mass accuracy and isotope ratio deviation

---

## Background

- High correctness in compound formula identification requires mass accuracy within 3 ppm and a maximum of 5% absolute isotope ratio deviation.  

- Ion suppression and peak coalescence can reduce mass accuracy in Orbitrap mass spectrometers. Ion count can reduce mass accuracy in Q-TOF mass spectrometers.

- Saturation of detector can affect the experimental isotopic ratio. Increased resolution appeared to increase isotopic distribution error.  

---

## Research Method

- Analyze mass accuracy and absolute isotope ratio deviation in a set of standards covering a large mass and retention time range. The standards are added to complex sample matrices: apple juice, yogurt, banana, infant food formula in 4 concentrations from low to high.

- Lock mass calibration: Lock mass calibration uses a “lock mass” of an ion that is present throughout the study to recalibrate for mass shift.  

- Mass accuracy: (mz_theo - mz_obs)/mz_theo in ppm.
- Isotope ratios calculated for A+1 and A+2 peaks
  - absolute isotope ratio deviation: % change in abs(RIA_theo - RIA_measured)  
  - RIA: (intensity_A+1/intensity_A)*100%  
  - RIA error: (RIA_exp - RIA_theo)/RIA_theo * 100%

---

## Conclusions

---

### Mass accuracy

- For orbitrap, the mass accuracy is within 3 ppm.
- Sample matrix does not influence mass accuracy.
- Mass accuracy can worsen if peak coalescence or ion suppression of a nearby co-eluting peak occurs.
- Orbitrap mass accuracy not influenced by intensity.
- Lock mass calibration improves mass accuracy, but when the ion cannot be detected due to electrospray ion suppression, the software made a mistake.
- Q-TOF mass accuracy shift could be as large as 40 ppm. After lock mass calibration it was less than 4 ppm. High ion counts is necessary to reduce the interference from background ions.
- Higher mass accuracy in Q-TOF can be obtained if an internal calibrant is injected at the beginning of every run.

---

### Isotopic ratios

- Absolute isotope ratio deviation worsens as amount of sample and signal intensity decreases.
- Orbitrap has smaller deviation under low intensity settings at the risk of introducing interference.
- With sufficient monosisotopic peak intensity, the deviation can be less than 5% for both orbitrap and Q-TOF.
- RIA error is higher in Q-TOF than in Orbitrap, and is generally lower under low intensities. The monoisotopic peak intensity should be higher than 1e5 to have absolute ratio deviation less than 5%.

---

### Others

- Longer chromatographic runs and high monoisotopic peak intensity are required for minimizing errors caused by interfering compounds.
- Co-elution impedes the detectability of target compounds.
