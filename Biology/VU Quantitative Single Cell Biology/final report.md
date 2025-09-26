# final report draft

## Methods

### Fluorescence Time-Lapse Imaging

Strain YET911 was tagged with mScarlet (RFP) at the GAL1 locus. Two pre-cultures—one in 2% glucose and one in 2% raffinose—were transferred to agarose pads containing 0.2% galactose. The RFP channel and GFP (background fluorescence control) were imaged every 15 minutes. Cells are segmented from the resulting images and tracked across frames. The centroids and mean and standard deviation of fluorescence intensities were calculated for the identified cells. For analysis, each transition was aligned at time 0 and truncated to 210 minutes (glucose→galactose) or 225 minutes (raffinose→galactose) to ensure equal duration.

### Automated Colony Detection and Tracking

Scatter plots were made using the provided cell centroids (x, y) and areas. OpenCV's contour detection algorithm was applied to identify globs formed by overlapping circles. Starting colonies were identified in the first frame. After identifying each colony in the first frame and calculating its centroid, new cells in subsequent frames were assigned to colonies by minimizing Euclidean distance to existing centroids.

## Results

### Slower GAL1 Induction Following Glucose Pre-Culture

Figure X1: Time courses of (A) total cell area, (B) total RFP intensity, and (C) cell number following a shift from glucose (blue) or raffinose (red) to galactose.

Figure Supp X1: Correlation of single-cell size and RFP intensity. Scatter plot of individual cell area versus RFP fluorescence under raffinose→galactose (A) and glucose→galactose (B) shifts at frame 0.

Figure Supp X2: GFP fluorescence controls. (A,B) Total GFP intensity over time for raffinose→galactose (left) and glucose→galactose (right). (C,D) Single-cell GFP traces for the two transitions.

Cells pre-cultured in glucose exhibited a significantly longer plateau before increasing total area, RFP fluorescence, and cell number, whereas cells pre-cultured in raffinose began expanding with minimal delay (Figure X1). Furthermore, although both conditions started with similar metrics, cells transferring from raffinose yielded more than triple the total RFP signal than the cells transferring from glucose, despite only modest increases in area (<20%) and cell count (< 40%). This indicates that elevated RFP arises from stronger GAL1 activation and not merely from higher cells numbers. As cell area and RFP intensity are uncorrelated (Figure Supp X1), greater cell area can be ruled out the the cause of fluorescence increase. The GFP fluorescence of raffinose pre-culture was about 20% higher than that of glucose pre-culture, likely reflecting its greater cell area and number (Figure Supp X2A-B).

### Single-Cell Dynamics Reveal Division Patterns and Induction Delay

Figure X2: Single-cell measurements over time for glucose→galactose (left) and raffinose→galactose (right): (A, B) cell area traces; (C, D) RFP intensity traces.

Figure Supp X3. Frequency analysis of cell-division cycles. Power spectra from Fourier transforms of single-cell area time series in (A) raffinose→galactose and (B) glucose→galactose transitions.

Single cell area traces show upper size limits that are revisited periodically by the cells, likely indicative of cell division cycles (Figure X2A-B).  Fourier transforms of the single cell traces reveal higher frequency oscillations in the raffinose pre-culture condition (Figure Supp X3), indicating faster cell cycles that lead to its greater cell number (Figure X1C). Notably, glucose-pre-cultured cells maintained a larger mean size reflecting faster initial growth rate on glucose compared with raffinose.

Single cell RFP traces reveal a induction delay in glucose-pre-cultured cells of about 60 minutes demonstrating catabolite repression, while almost no delay was observed in the raffinose-pre-cultured cells (Figure X2C-D). In contrast, GFP remained approximately constant across both conditions with minor fluctuations, confirming that observed RFP changes are specific to GAL1 activation (Figure Supp X2C-D).

### Increased Intra- and Inter-Cellular Variability with GAL1 Activation

Figure X3: Scatter of single-cell RFP standard deviation versus mean for raffinose→galactose (left) and glucose→galactose (right). Color gradient indicates cell area.

In both transitions, higher mean RFP correlates with increased standard deviation, reflecting more uneven distribution of fluorescence signals within the cells (Figure X3). However, it should be noted that in smaller cells sub-cellular heterogeneity cannot be resolved due to resolution limits. Across the population, RFP standard deviation also broadens with the mean intensity. This inter-cellular heterogeneity is the result of accumulating stochasticity as more GAL1 gene is expressed (Figure X3).

### Colony-Level Response Trajectories

> Time series clustering still needs to be done for this part, will lead to more figures and interpretations.

Figure X4: Colony-level RFP over time for raffinose→galactose (left) and glucose→galactose (right). (A,B) average per-cell RFP; (C,D) total RFP. Color denotes the corresponding metric at time 0.

Figure X5: Colony-level cell area over time for raffinose→galactose (left) and glucose→galactose (right). (A,B) average per-cell RFP; (C,D) total RFP. Color denotes the corresponding metric at time 0.

Figure Supp X4: Colony cell-number trajectories. Total cell count versus time for each colony under (A) raffinose→galactose and (B) glucose→galactose transitions. Line color reflects the cell count at time 0.

Colony identification found 60 raffinose pre-culture colonies and 53 glucose pre-culture colonies at time 0. In raffinose, colonies showed uniform average RFP induction, while in glucose, two clusters of trajectories were observed between the colonies, reflecting bet-hedging (Figure X4A–B). Furthermore, the delayed induction observed in Figure X2D was not randomly distributed in cells but coordinated within the colonies. 

High initial average RFP did not predict final average levels, since those early high values often arose from single-cell colonies. In contrast, colonies with high initial total RFP remained at the top, reflecting that larger colony size produces consistently greater fluorescence (Figure X4C–D; Supp X4).

Similar trends were observed in cell area: average area rankings shifted at the end due to single-cell colonies, but total colony area rankings remained consistent (Figure X5). A slight declining trend were found in both the average area over time plots. Since the total cell number increases over time for the colonies (Figure Supp X4), it reveals that bacteria increase their colony size by producing more but smaller cells rather than fewer larger cells.

### Division Partitioning Unaffected by Catabolite Repression

> can do a t test for this to be more robust

Figure X6: Mean RFP fluorescence over time for (A, B) daughter and (C, D) mother cells, and (E, F) daughter/mother ratio under raffinose→galactose (left) and glucose→galactose (right) transitions.

For each frame, daughter cells were defined as cells that newly appearing cells, and the remaining cells were defined as mother cells. Both mother and daughter RFP intensities rose over time (Figure X6A–D). However, the daughter/mother fluorescence ratio remained stable and comparable across both transitions (Figure X6E–F), indicating that partitioning mechanisms operate independently of pre-culture conditions, cell size, division rate, and induction dynamics.


$$
\langle f \rangle \;=\; 
\frac{\displaystyle \sum_{k=1}^{K} f_k \,P(f_k)}
     {\displaystyle \sum_{k=1}^{K} P(f_k)} 
$$
where \(f_k\) are the positive frequencies and \(P(f_k)\) is the power at each \(f_k\).

Time-series clustering of colony-averaged RFP traces (Figure X4B) identified two distinct temporal clusters in the glucose→galactose condition, corresponding to faster- and slower-adapting colonies (Figure X7A). These clusters were not spatially segregated across the imaging field. Mean RFP intensity at both the colony and single-cell levels did not significantly differ between clusters (Figure Supp X6B–C; p > 0.05, Wilcoxon rank-sum test). However, colonies in the faster-adapting cluster had significantly higher initial cell counts (Figure X7B; p < 0.05), suggesting that larger starting populations may enable greater phenotypic diversity and increase the likelihood of containing early-adapting cells. This early advantage translates into sustained growth benefits, as these colonies consistently exhibited greater total area and higher cell numbers throughout the experiment (Figure X7C–D).

Evolution-driven Spatial-temporal Heterogeneity in Catabolite Repression in Yeast Galactose Adaptation

Yeast Galactose Adaptation Reveals Single-Cell Spatiotemporal Heterogeneity in Catabolite Repression Shaped by Evolution



I need you to write a discussion section for my report using the information I provide below. The following text outlines findings (FOUND) and interpretations (INTERPRETATION) for each result section of my report. The old discussion section contains things that should be included (INCLUDE) in addition. The information is in bullet points but I want my discussion section to be in several paragraphs. The new discussion should follow the order of the result sections, first sumarize findings and then explain the interpretations of each section. Furthermore, repeated findings should not be written twice but only mentioned briefly. It's also important that the discussion of interpretations should establish and follow a coherent storyline explaining how yeast adapt to carbon source change following the logical order of evolutionary pressure causes cells to optimize for growth, which causes catabolite repression, which shapes the observed findings, and finally the mechanistic explanations for the findings, which are in the INCLUDE part of the information I provide you. The INCLUDE part should be incorporated as much as possible. Also make sure not to change the references made. The language and tone of the discussion should follow the same description I gave you.

## Points to be made in discussion

### Lag phase of cells transitioned to a different carbon source depends on their pre-growth condition

- FOUND: S. cerevisiae grows the fastest on glucose followed by galactose and raffinose at similar levels.
- FOUND: Glucose is the preferred carbon source: pre-growth on glucose has longer lag phase for transitioning to raffinose or galactose; transitioning from raffinose or galactose to glucose has short lag phase.
- INTERPRETATION: A longer lag phase after transitioning from glucose to raffinose or galactose reflects the evolutionary strategy that has been naturally selected through evolution: cells that wait for glucose to come back can resume growth faster and achieve a higher growth rate, thus increasing its fitness if glucose becomes available again.
- INTERPRETATION: A shorter lag phase following transitioning from raffinose or galactose to glucose shows that cells have a strong preference for glucose. It demonstrates how strongly glucose presence inhibits gene expression for raffinose and galactose metabolism via catabolite repression.

### Cells transitioned from raffinose show faster GAL1 induction

- FOUND: bimodal distribution in cell size and morphology in cells transitioning from raffinose to galactose, but not in cells transitioning from glucose to galactose. In later time points the bimodal distributions become unimodal.
- INTERPRETATION: uncertain why bimodal distribution of cell sizes in the beginning;  it could be due to more stochasticity in gene expression and enzyme reactions specific to raffinose metabolism leading to more diverse subpopulations. converging to unimodal distribution in later time points suggest galactose metabolism involves less stochasticity. however, it could also be due to experimental artefacts in the raffinose pre-cultured cells that were somehow resolved after transitioning to galactose.
- FOUND: GAL1 promoter + GAL1 gene and GAL1 promoter + DOA1 gene both had increased gene expression levels in raffinose to galactose transition but did not increase significantly in glucose to galactose transition
- FOUND: transitioning to glucose had much longer induction times. only after 16 hours are gene expression levels comparable to those in raffinose to galactose transition condition.
- FOUND: time to galactose induction and total increase in fluorescence appear not related to galactose concentration.
- INTERPRETATION: longer lag phase in glucose-to-galactose transition is observed again. Furthermore, while both controlled by GAL1 promoter, the fluorescent levels of GAL1 gene is higher than those of the DOA1 gene, suggesting additional regulatory mechanisms that increases GAL1 gene expression.

### Cells grown in raffinose show more heterogeneity in GAL1 expression before transition to galactose

- FOUND: again, higher levels of GAL1 mRNA were observed for cells transferred from raffinose to galactose than when transferred from glucose
- FOUND: cells grown on raffinose without transitioning has higher heterogeneity in GAL1 mRNA counts
- FOUND: cells transitioned from raffinose to galactose have higher variance in GAL1 mRNA expression
- INTERPRETATION: more GAL1 expression means more random events and hence more variance in expression level; anther source of noise is lack of strong catabolite repression when growing on raffinose. so GAL1 gene is less repressed and can be expressed more due to chance.

### Stronger GAL1 activation in raffinose pre-cultured cells

- FOUND: Again, delayed galactose metabolism induction in glucose to galactose transition
- FOUND: about triple RFP fluorescence signal while only modestly higher cell number and area between raffinose to galactose and glucose to galactose conditions
- INTERPRETATION: the increased RFP fluorescence was not just due to higher cell area and cell number but stronger GAL1 expression in raffinose to galactose condition - more proteins are produced

### Single-cell dynamics reveal division patterns and induction delay

- FOUND: Both conditions have almost exactly the same power weighted mean frequency
- INTERPRETATION: the different transitions and catabolite repression do not alter the underlying cell cycle; the cell cycle is tightly regulated

### Colony identification uncovers diverse response patterns in glucose pre-cultured cells

- FOUND: raffinose-to-galactose condition had more uniform colony mean and total RFP intensity curves while glucose-to-galactose condition had two distinct clusters of trajectories
- INTERPRETATION: clusters of trajectories show phenotype diversification in glucose-to-galactose condition; the colony clusters also demonstrate that the delayed induction observed in glucose-to-galactose condition for single cells was not randomly distributed but coordinated within the colonies.
- FOUND: mean area per colony decreases while total area and cell number per colony increases
- INTERPRETATION: Since the total colony area and cell number increases over time for the colonies, it reveals that yeast increase their total colony area by dividing more frequently to produce more but smaller cells rather than less frequently and grow fewer but larger cells - an evolutionary strategy that could confer better fitness.

### Colony size influences adaptation time to galactose in cells transferred from glucose

- FOUND: 2 temporal clusters identified from average RFP trace for the colonies. colonies that adapt to galactose faster transitioning from glucose have higher initial cell counts
- INTERPRET: larger starting populations may enable greater phenotypic diversity and increase the likelihood of containing early-adapting cells. This early advantage translates into sustained growth benefits, as these colonies consistently exhibited greater total area and higher cell numbers throughout the experiment.
- FOUND: increased inter- and intra- cellular heterogeneity in GAL1 expression as time progresses
- INTERPRET: From an evolutionary perspective, maintaining a high mean GAL1 expression with minimal variance could improve growth efficiency. However, the energetic cost of tightly regulating expression likely outweighs the marginal gains in growth, thereby favoring the observed rise in both intra- and inter-cellular heterogeneity over time.

### Division partitioning unaffected by catabolite repression

- FOUND: daughter/mother cell fluorescence ratio remain stable and comparable across conditions
- INTERPRETATION:indicating that partitioning mechanisms operate independently of pre-culture conditions, cell size, division rate, and induction dynamics.

### OLD DISCUSSION

- INCLUDE: Cells pre-grown on raffinose entered the GAL1-induced state far more quickly than glucose-grown cells. This observation may be attributed to the multilayered catabolite-repression program that typically keeps GAL genes silent in the presence of glucose. Glucose reduces \textit{GAL} cluster expression by downregulating Gal4, so cells without this repression may display more noisy \textit{GAL} cluster expression which can shorten the lag phase duration \parencite{Johnston01061994}. A second, subtler influence is cellular physiology: theory and single-cell data show that gene-state switching becomes noisier as growth rate declines, meaning the slower growth on raffinose should increase stochastic variability \parencite{Groot2023}. Greater noise could, in principle, delay commitment, yet GAL2 -- the high-affinity galactose transporter -- is already expressed heterogeneously in raffinose because its promoter escapes repression outside glucose. Promoter studies reveal that MIG1- and GAL80-dependent feedback convert the GAL response from binary in glucose to graded in non-repressing sugars, sharpening this basal heterogeneity \parencite{Biggar2001, Ramsey2006} . Thus, while enhanced noise in slow-growing cells may modulate single-cell timing, the dominant driver of the shortened induction lag after a raffinose pre-culture is the relief of glucose-specific catabolite repression.
- INCLUDE: Single-cell work on other nutrient transitions shows that such lags often stem from amplitude-rather than timing-based noise in transcription \parencite{Schwabe2014} , and genome-wide proteomics confirms that environment-responsive genes, including the GAL regulon, sit at the noisy end of the expression spectrum \parencite{Newman2006}. This noise creates a fitness trade-off; strains that “pre-induce” GAL genes experience a growth penalty while glucose is plentiful but resume growth first when it disappears—a pattern typical of bet-hedging \parencite{Wang2015}. Compelling evidence that yeast really exploit this strategy comes from the discovery of two heritable metabolic states -- fast “recoverers” and slow “arresters” -- that spontaneously segregate and re-establish their proportions each generation, buffering populations against abrupt carbon starvation \parencite{BAGAMERY20204563}. Altogether, our measurements and these studies argue that stochastic gene-expression noise, coupled with partial inheritance of metabolic states, equips yeast with a basic hedging mechanism even though its evolutionary origins remain to be proven.
- INCLUDE: While population heterogeneity highlights cell-state differences, gene-intrinsic properties offer an additional layer of control, as indicated by a comparison of \textit{GAL1} and \textit{DOA1} expression. Even when \textit{GAL1} and \textit{DOA1} are placed behind the same promoter, \textit{GAL1} mRNA still accumulated more strongly. Three gene-intrinsic factors can explain this gap. First, the native GAL1-10-7 cluster, when induced, moves to nuclear-pore complexes and even self-clusters across chromosomes, which can promote its transcription \parencite{Brickner2016-dw}. This local enrichment of alleles, and perhaps transcriptional regulators, is absent for the solitary DOA1 cassette. Second, promoter architecture likely also affected expression of both genes. \textit{GAL1} and its neighbor \textit{GAL7} share nearly identical UASG (upstream activating sequences for galactose) arrays, and single-molecule tracking shows that tandem Gal4 binding sites sustain longer, higher-frequency transcriptional bursts than isolated sites, a property that would inflate GAL1 output even when the upstream core promoter is held constant \parencite{Pomp2024} . Third, gene length sets an upper limit on throughput—GAL1 is ∼1.4 kb whereas DOA1 exceeds 4 kb, so the longer ORF simply ties up RNA-polymerase II for roughly three times longer per transcript \parencite{Conrad2014}. Reviews of carbon-source-responsive promoters underscore that this cluster geometry plus multiple UAS copies makes the GAL set among the strongest natural expression systems in yeast \parencite{Weinhandl2014}. Altogether, spatial positioning, burst kinetics, and ORF length explain why GAL1 expression still outpaces DOA1 even hours after induction, when steady state should, in principle, have been reached.