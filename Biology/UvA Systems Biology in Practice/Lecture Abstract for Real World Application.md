---
title: ""
author: ""
geometry: top=0in, bottom=0in, left=0.5in, right=0.5in
fontsize: 11pt
papersize: a4
---
## Lecture Abstract

Author: Chuyao Wang

### Background

Bacterial fermentation is commonly applied in the food industry. For example, during their fermentation, bacteria produce acids that change the flavor and texture of milk and meat to make yogurt, cheese, and sausage. Some bacteria, such as yeast, produces $CO_{2}$ and alcohol during fermentation that can be utilized to make baked goods. At the molecular level, fermentation revolves around the metabolism network of bacteria. The inputs sugar and protein are converted in metabolic reactions into the outputs ATP, organic acids, ethanol, amino acids, B vitamins, anti-bacterial compounds, flavor compounds, and oil and fatty acids.

Wild strains are hardly suitable for efficient production of desired compounds at the industry level. A systems biology approach can often be employed to increase the yield and change the direction of metabolic fluxes. In this lecture 3 such applications are discussed: increasing growth rate for _Lactobacillus plantarum_ that produces anti-fungal compounds, redirecting metabolic flux for _Lactococcus lactis_ that produces flavor compounds, and increasing fatty acid yield in _Cryptococcus curvatus_. A technical economic analysis (TEA) framework is introduced at the end that models the economic feasibility of a microbial production factory.

### Investigating growth arrest in _Lactobacillus plantarum_

_Lactobacillus plantarum_ is a bacteria strain that is used to produce a natural preservative against fungal growth on food products and in culture medium. However, a delay in its growth rate that happened consistently after a fixed amount of fermentation time, was independent of $OD_{600}$ or pH, and was only in aerobic culture was detected. To pinpoint the cause, transcriptomics analysis was done for the bacteria culture before and after the growth arrest. In a metabolic model, the up-regulated genes after growth arrest coded for $CO_{2}$ producing enzymes, and the down-regulated genes after growth arrest coded $CO_{2}$ consuming enzymes. Hence, the researchers hypothesized that $CO_{2}$ is an important compound for bacteria growth such that its removal from the culture caused the growth arrest, and growth resumed after the bacteria produced enough $CO_{2}$ by itself. Follow-up experiment that flushed in gas with $CO_{2}$ indeed prevented growth delay.

### Metabolic engineering to increase diacetyl production

Diacetyl is a buttery flavor compound that has high economical value. It is produced from _Lactococcus lactis_ fermentation of citrate during milk fermentation in trace amounts. The key challenge is to redirect the metabolic flux such that pyruvate, a key intermediate, is not converted into lactate but into diacetyl. The naive approach to knockout the lactate dehydrogenase stopped lactate production but increased acetoin rather than diacetyl production. To identify a better target, a kinetic metabolic model including enzyme affinity constants and rate constants were employed. Control coefficients were calculated for the enzymes, and over-expression of NADH oxidase (NOX) was predicted to most positively influence diacetyl production. An experiment that knocks out the acetoin producing enzyme _aldB_ while over-expressing NOX led to up to 75% conversion to diacetyl from sugar.

### Oil producing bacteria

Palm oil is consumed globally, but its high environment cost and climate requirement limits its market potential. The company No Palm Ingredients is developing microbe based oil using a yeast strain called _Cryptococcus curvatus_, an oil-producing bacteria. The PhD. project is about tailor made microbial oil that has custom compositions. The environmental factor C/N ratio that induces oil storage was chosen. Other factors such as temperature, pH, and oxygen concentration were also examined. The bacteria were grown under different conditions to analyze growth, total lipid yield, and oil composition. Differential gene expression was then performed for high and low oil producing conditions, and genes related to fatty acid biosynthesis were identified. Three genes were chosen and over-expressed, leading to increased oil content. Other components such as amino acids, vitamin, and biotin also affected lipid production. In the end, oil production was brought up from 20% to 56%.

### Technical economic analysis (TEA) 

TEA is used for designing a chemical factory that is cost-effective. It is a model with many parameters such as number of reactors and volume of fermentation that is economically feasible. For the No Palm Ingredients company, it allows calculating price per kg oil produced. The oil must be about the same price as commercially available palm oil for the company to thrive. One strategy to reduce cost is low capEX: use cheaper equipments that offer less control but bring down the oil cost.