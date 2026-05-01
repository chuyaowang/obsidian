# Blueprints for Breakthroughs: Creating a Multiomic Future of Biological Discoveries and Medical Advances

**Speakers:**  
- Eric Green, MD, PhD — Chief Medical Officer, Illumina; former Director (32 years), National Human Genome Research Institute (NHGRI), NIH  
- Bodour Salhia, PhD — Department Chair and Professor of Cancer Biology, Keck School of Medicine, USC  

**Host:** Kevin Davis, GEN Editorial Director  
**Session type:** Sponsored conversation (Illumina)  
**Event:** State of Multi-omics and NGS 2026 Summit

---

## Background

Multi-omics refers to the simultaneous or integrated measurement of multiple molecular layers within the same biological system — typically combining two or more of genomics, transcriptomics, epigenomics, proteomics, metabolomics, and spatial information. While researchers have attempted data integration for decades (earlier termed "integrated genomics analysis"), practical multi-omics at scale became achievable only recently, driven by convergence of several enabling factors: the dramatic cost reduction of next-generation sequencing, the commercialization of multi-analyte spatial platforms, improvements in computational and analytical frameworks, and — increasingly — AI-assisted data interpretation.

The **epigenome** refers to heritable modifications to the genome that regulate gene expression without altering DNA sequence: DNA methylation, histone modifications, chromatin accessibility, and non-coding RNA. Epigenomic regulation is pervasive, tissue-specific, and dynamic — but its study has historically lagged behind genomics and transcriptomics because the assays were technically more demanding, the reference frameworks less mature, and the data integration more complex. Five-base sequencing (simultaneous variant calling and CpG methylation calling from the same sequencing library) represents one frontier in epigenomics.

**Translational research** bridges basic scientific discoveries and clinical application. Multi-omics is positioned as a key enabler of this translation: by capturing multiple regulatory layers simultaneously, researchers can move from biomarker discovery in tissue to clinically deployable tests more efficiently than with single-analyte approaches.

---

## Section 1: Eric Green's Transition from NHGRI to Illumina

Green's transition was framed not as a planned career move but as an organic fit. After 32 years as NHGRI Director — encompassing the completion of the Human Genome Project, the ENCODE project, and the development of the NHGRI genome sequencing program — he spent time consulting in academia before Illumina approached him. He described it as "just feeling right," noting that the conversations he was having at Illumina about genomics and multi-omics were the same conversations he had been having at NHGRI. Three months into the role at the time of the talk, he was drawing on parallel experiences across academia, government, and now the private sector.

The relevance of this biographical framing: Green brings a perspective shaped by decades of public-sector genomics investment and a view of multi-omics as both a scientific necessity and a policy challenge. His involvement with Illumina signals the company's ambition to position itself as the institutional architect of the multi-omics era rather than merely a sequencing technology vendor.

---

## Section 2: What Multi-omics Promises — and What Remains Overhyped

**Kevin Davis's question:** What's one promise of multi-omics that is now real, and one area that remains overhyped?

**Eric Green on the promise:** Each additional omic layer added to genomic data produces an "aha moment" — new biological insight that could not have been obtained from the single-omic view. He pushed back on the idea of asymptotic returns: "It's not even getting asymptotic... there's so much more because there's so many more dimensions we could look at." The field is past the point of no return; multi-omics is the direction of travel.

On overhype: the idea that collecting large amounts of multi-omic data and handing it to AI will automatically produce insights. "The overhype is how difficult the data science and analysis aspects of this are going to be, and the more you layer on and the more multi-dimensional it gets, the greater the challenge." He was careful to add that this is not a reason to stop — it is a challenge that computational biology and AI advances will address — but the expectation of automatic insight from raw data accumulation is unrealistic.

**Bodour Salhia on the promise:** The transformation is not just in what data can be collected but in *how*. Earlier attempts at integrated genomics required multiple different machines, laborious assay harmonization, and difficult analytical reconciliation of heterogeneous data types. Current multi-omics platforms are increasingly "one-stop shops" that simplify workflow, reduce the need for harmonization, and democratize access by lowering costs. This accessibility is the transformative promise of the current era.

On remaining complexity: regardless of improved platforms and AI tools, the fundamental challenge of *interpretation* — knowing what question to ask, whether to take a top-down or bottom-up approach, how to make sense of the answers — remains deeply human work. "It's a bit of a wild card still in that area if you're not deeply embedded in it."

---

## Section 3: Where Multi-omics Delivers Impact First

**Salhia** described a spectrum from passive to active use of multi-omics:

*Passive ("fishing expedition"):* Collect as many data layers as possible on a system of interest and let patterns emerge — analogous to stamp-collecting. This is a legitimate early-phase discovery strategy but becomes harder to interpret as dimensionality increases.

*Active (hypothesis-driven):* Use a specific biological question to determine which additional layers of information are most likely to be informative. As an example from Salhia's lab: in developing biomarkers for early detection of ovarian cancer, the team observed that a methylation signal present in tissue was being lost in plasma. Adding proteomics data allowed them to investigate whether the signal could be retained in a different analyte. Adding spatial information clarified which cell populations were driving or obscuring the signal. This iterative, question-driven approach makes multi-omics tractable and biologically interpretable.

Impact areas: early diagnosis, patient stratification, target discovery, therapy response prediction. Salhia's view is that multi-omics can contribute across all of these, and the value depends on matching the question to the right combination of modalities.

**Green** suggested impact will follow a familiar historical arc: early wins in basic and translational discovery research, then clinical translation of the easiest and most validated findings. He sees population-scale multi-omics studies as a near-term inflection point, but clinical adoption of multi-omics panels will follow, not precede, demonstration of validity.

---

## Section 4: When Multi-omics Changes the Answer — Concrete Examples

**Salhia's ovarian cancer example:** The methylation signal marking malignancy is present in tissue but degrades in plasma. Proteomics helps retain or proxy the signal. Spatial information reveals which cell types are generating the signal and whether neighboring cells are amplifying or suppressing class separation. This is the practical workflow: integrating multiple modalities not because it is fashionable but because each layer resolves an ambiguity the others cannot.

**Green's rare genetic disease framing:** The genomic basis of ~6,000 of ~10,000 rare genetic diseases has been identified; the remaining ~4,000 have been resistant to purely genomic explanations. The reason, increasingly, is that causal variants are not in protein-coding sequence. They may be non-coding variants causing **cryptic splicing** detectable only by transcriptomics, or variants altering epigenomic marks with downstream regulatory consequences detectable only by epigenomics. The only way these diseases are solved is by going to another omic layer.

Green used this to reframe why multi-omics is not merely fashionable but scientifically necessary: "We're here for two reasons — one is a technology we can; the other is that we *must*, because we're getting caught by complexity." The genome project's original assumptions (most information in genes, non-coding DNA less important, epigenetics a secondary concern) have been repeatedly falsified. Each falsification points to a new omic layer as necessary.

---

## Section 5: Underappreciated Data Types

**Green:** Epigenomics. Not because it lacks recognition but because "we're just scratching the surface of the epigenomics landscape." Single-cell and spatial genomics are revealing that organs we studied by grinding up tissues are actually composed of cells in dramatically different states. The dimensionality that single-cell and spatial technologies expose is a direct consequence of recognizing that epigenomic regulation is operating cell-by-cell.

**Salhia:** The integration layer — specifically, how one omic truly controls another. We can measure DNA methylation and gene expression, but capturing the *mechanistic relationship* between them (which methylation event controls which gene in which cell) remains technically difficult. The possibility of **five-base sequencing** (simultaneous variant and methylation calling from a single molecule) is exciting because it would allow causal rather than correlative relationships to be resolved from the same molecule. Temporal dynamics — capturing how these relationships change over time — is another underappreciated dimension.

---

## Section 6: Is Oncology the Dominant Application Domain?

Salhia acknowledged that oncology has led multi-omics adoption — the molecular complexity of cancer, the availability of large biobanked cohorts (TCGA, ICGC), and the clinical imperative to stratify patients all made it the natural first arena. But she argued forcefully that multi-omics is equally or more valuable in other disease areas:

- **Rare diseases:** Multi-omics may resolve diagnostic cases where single-nucleotide variants alone don't explain the phenotype — particularly important where mutations account for incomplete disease expressivity.
- **Neurological diseases:** Acquired mutations contributing to neurodegeneration are now recognized thanks to omics. Single-cell and spatial genomics are essential given the cellular heterogeneity of brain tissue.
- **Immunological and cardiovascular diseases:** Both are molecularly complex and would benefit from the layer-by-layer insight multi-omics provides.

Green noted that cancer's advantages (visible molecular diversity, established clinical trial infrastructure, existing biomarker frameworks) have made it a proving ground, but the lessons are generalizable.

---

## Section 7: AI and Trust in Translational Programs

**Salhia's requirements for trusting AI outputs in translational programs:**
1. Models must be **interpretable** and **biologically grounded** — outputs must be traceable to underlying molecular mechanisms, not just statistical patterns.
2. Models must be **validated in real-world datasets**, not just held-out test sets from the same cohort.
3. **Training data quality is paramount:** "garbage in, garbage out." The right samples, the right question, appropriate class labels.
4. **Education:** Graduate programs must now teach not only generative AI but the machine learning classifiers used for biological applications. Understanding model assumptions is becoming a core scientific literacy.

Salhia noted that AI models in translational genomics fail more often than appreciated because researchers don't fully understand what they're optimizing for, or because the training cohort doesn't represent the real-world clinical population. These failures often happen quietly rather than being reported.

---

## Section 8: Funding Multi-omics — Practical Guidance

Green, drawing on his experience administering hundreds of millions of dollars in NHGRI grants, framed the funding challenge as a partnership problem: the private sector must deliver affordable and accessible technologies (Illumina is committed to this), and the public sector must provide demonstration projects that validate multi-omics' clinical utility to justify investment.

He highlighted the **MOHD (Multi-omics of Human Disease)** consortium — one of the last initiatives he launched as NHGRI director (approximately three years before this talk), now running with contributions from additional NIH institutes. MOHD was explicitly designed as a demonstration project: investigators must use genomic data plus at least one additional omic layer and demonstrate new biological or clinical insights. The hypothesis is that once pilot projects prove the value of multi-omics, other institutes will follow with their own investments.

Salhia's practical advice for labs: cost reduction, ease of use, streamlined workflows, and education. Multi-omics will penetrate more broadly when researchers who are not yet using it can understand what questions it enables, not just what technologies it involves.

---

## Section 9: Five-Year Outlook

**Salhia:** Multi-omics will become standard practice — analogous to where next-generation sequencing is today. Data harmonization and interpretation tools will improve through experience. The analogy to early sequencing is apt: it moved from being a specialized capability to a garden-variety assay in many labs relatively quickly, and multi-omics is on a similar trajectory given its broader technological and conceptual foundation.

**Green:** Three concurrent trends: (1) population-scale multi-omics studies that are "seismic in scale," enabled by widespread accessibility; (2) individual investigators doing sophisticated multi-omics as a routine part of their research; and (3) a small number of exemplars where multi-omics data is sufficient and validated for **clinical test deployment** — most likely in cancer first. Clinical adoption will not be "wholesale everywhere" within five years, but proof-of-concept clinical tests will exist.

---

## Summary

This conversation between Eric Green and Bodour Salhia offered complementary perspectives from a genomics policy veteran and a translational oncology researcher. The central thesis was that multi-omics is scientifically necessary — not merely technologically possible — because biological complexity has outrun the explanatory power of any single molecular layer, and that the practical barriers to multi-omics adoption (cost, workflow complexity, data science challenges, education gaps) are progressively being addressed.

Key convergence points between the two speakers: data science and interpretation remain the hardest problem even with improved platforms and AI tools; AI outputs require interpretability, biological grounding, and training data quality to be trusted in translational contexts; and the trajectory of multi-omics will follow the sequencing curve — rapid democratization in research settings, followed by carefully validated entry into clinical practice. The MOHD consortium represents a deliberate public investment in demonstrating the translational value of multi-omics that is intended to de-risk subsequent adoption by other NIH institutes and eventually clinical settings.

The most intellectually interesting tension in the conversation was Green's observation that two forces are driving multi-omics simultaneously: the technological "we can" and the scientific "we must." The latter — the repeated humbling of reductionist assumptions about the genome — may be the more durable motivation.
