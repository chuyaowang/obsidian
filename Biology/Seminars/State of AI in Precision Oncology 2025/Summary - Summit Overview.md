# The State of AI in Precision Oncology 2025 — Summit Overview

**Format:** Virtual Summit  
**Sponsor:** Natera  
**Journal:** *AI in Precision Oncology (AIPO)*  
**Host/Moderator:** Doug Flora, MD — Executive Medical Director, Yung Family Cancer Center, St. Elizabeth Healthcare; Editor-in-Chief, *AIPO*

---

## Speakers

| Talk | Speaker(s) |
|---|---|
| Fireside Chat: Cancer Screening — Hype vs. Reality | Doug Flora, MD · Elizabeth (Betsy) O'Donnell, MD (Dana-Farber / Harvard) |
| Keynote: Realizing the Promise of Biology's Century | Amy Abernethy, MD, PhD (Highlander Health; former FDA) |
| Fireside Chat: State of AI in Community Oncology | Lucio Gordan, MD (Florida Cancer Specialists) |
| Pioneering Patient-Specific Treatments Using AI *(sponsored)* | Helio Costa, PhD (Natera / Stanford) |
| Adventures in AI, Informatics and Publishing | Doug Flora, MD · Isaac (Zak) Kohane, MD, PhD (Harvard / NEJM AI) |
| AI and Breast Cancer Detection | Doug Flora, MD · Constance (Connie) Lehman, MD, PhD (MGH / Harvard; Clarity) |
| Fireside Chat: AI in Oncology — The View from 2030 | Doug Flora, MD · David Penberthy, MD (UVA; ACCC) |

---

## Introduction

The State of AI in Precision Oncology 2025 summit convened a cross-disciplinary group of physician-scientists, informaticists, community oncologists, diagnosticians, and health policy experts to take stock of where artificial intelligence stands in cancer care — and where it is headed. Across seven sessions spanning early detection, clinical practice, publishing, drug discovery, and health policy, a set of powerful convergent themes emerged. Rather than summarizing each talk individually, this overview synthesizes those themes across the full day, comparing perspectives, identifying consensus and tension, and drawing out the summit's collective argument about the future of oncology.

---

## Theme 1: The Paradigm Shift — From Reactive Treatment to Proactive Interception

If there is a single intellectual heartbeat running through every session of this summit, it is this: oncology must move from its current posture — reacting to advanced disease with sophisticated but often ultimately insufficient therapies — toward a proactive model that finds cancer in its earliest chapters, intercepts precursor conditions, and ultimately prevents cancers from developing at all.

This argument was made from multiple angles and with different kinds of evidence. O'Donnell (cancer screening) framed it through the lens of plasma cell dyscrasias: multiple myeloma has a defined precursor state (MGUS → smoldering myeloma), and the recently FDA-approved use of daratumumab in high-risk smoldering myeloma — showing both progression-free and overall survival benefit in the ECILA trial — demonstrates that early intervention works. The same logic, she argues, must now be applied systematically to solid tumors. Flora's metaphor of "reading the first chapter of the book rather than chapter four" recurred throughout the day.

Lehman (breast cancer detection) made the same argument from imaging. Her Clarity platform — the first FDA de novo–authorized AI tool to predict future breast cancer risk from mammography — exemplifies a shift in the radiologist's role from detecting existing cancers to predicting and preventing future ones. She presented preliminary data showing that AI risk scores begin rising measurably five years before a breast cancer diagnosis, and that these scores change dynamically in response to interventions like tamoxifen or weight loss — creating a quantitative feedback loop for prevention.

Abernethy (keynote) placed this shift in the context of clinical research infrastructure: the current clinical trial system is built for late-stage disease, and Highlander Health's central bet is that longitudinal data assets can underpin a new generation of nested trials that follow disease from its earliest whispers. Penberthy (2030 vision) extended this to the economic argument: with cancer incidence projected to rise 50% by 2040, the system cannot afford to keep discovering and treating advanced disease at the current rate. Interception and prevention are not just clinically better — they are financially necessary.

The summit's consensus on this theme is broad and deep. The remaining challenge is not scientific conviction but translational execution: building the trials, the reimbursement pathways, and the clinical infrastructure to make proactive cancer medicine routine.

---

## Theme 2: Liquid Biopsy, ctDNA, and the Power of Molecular Signal

Circulating tumor DNA (ctDNA) and the tools built around it were a central technical thread running from the cancer screening talk through the Natera session and into multiple other conversations. The technology represents, in Flora's framing, the "next lens" after CT scans and MRI — a sensitivity of detection that operates at 10⁻⁵ to 10⁻⁶ cancer cells, far below what any imaging modality can see.

O'Donnell provided a conceptual framework: MCED tests use sequenced ctDNA from a blood draw, compared against AI-trained reference databases of what cancer DNA from different tissue types looks like, to screen for signals of malignancy. The field has progressed from binary ("signal detected / not detected") to probabilistic tissue-of-origin classification. The Pathfinder 2 study (Grail/Galleri) reported a positive predictive value of ~62% in a general population, up from ~40% in Pathfinder 1 — meaningful improvement, with more to come in higher-risk populations. O'Donnell's own clinical experience: 78% true positive rate among screened patients.

Costa (Natera) showed the other face of ctDNA technology: not population screening but personalized, longitudinal MRD monitoring via Signatera. Because Signatera tests follow a patient's unique tumor mutational fingerprint in blood over time, serial measurements reveal molecular dynamics — rising ctDNA as disease progresses, falling ctDNA as therapy works — that are quantitatively more sensitive than any imaging. Natera's dataset of hundreds of thousands of early-stage patients receiving serial Signatera tests is the foundation of their AI platform.

The difference in emphasis between these two approaches — population MCED screening vs. personalized post-treatment MRD monitoring — reflects genuine clinical diversity: MCED applies to healthy or at-risk people who may not have cancer; MRD monitoring applies to patients who have had cancer and are being surveilled. Both are driven by the same underlying technology and the same enabling capability: AI pattern recognition at a scale that makes needle-in-haystack detection tractable.

---

## Theme 3: AI as a Force Multiplier — Not a Replacement

Every speaker, without exception, made the same fundamental claim about AI's relationship to clinicians: AI will not replace physicians, nurses, pharmacists, or other healthcare professionals. The human-to-human element of care is irreplaceable. What AI replaces is the cognitive and administrative overhead that does not require that human connection.

Gordan (community oncology) made this argument most quantitatively. Ambient AI documentation tools reduce note time by 30–50%, cut after-hours charting by 45%, save ~4 hours per week per provider, and reduce burnout by 20–30%. AI order-checking and infusion verification reduce near-miss errors by 42% and infusion mismatches by 70%. AI biomarker auto-mapping improves guideline concordance from 71% to 89% and reduces time to drug selection by more than 50%. The framing he consistently used: AI is "flying the airplane" so the pilot can focus on what requires human judgment.

Abernethy (keynote) introduced the transparency-versus-invisibility tension that is arguably the central UX challenge of clinical AI: clinicians want to be able to audit AI reasoning ("show me the PDL-1 score and the trial that led to this recommendation") but they also don't want additional click fatigue. Her solution: performance monitoring infrastructure — a background "cockpit" that continuously validates AI accuracy and alerts the clinical team when a model drifts or underperforms, so that clinicians can trust the system is running well without checking it manually.

Penberthy (2030 vision) reframed this with the term "augmented intelligence" — human intelligence incorporated into machines, and AI enhancing human performance — arguing this framing is more accurate and more practically useful than "artificial intelligence replacing humans." His slogan, borrowed from Flora: we are "changing mundane to humane."

Kohane (publishing) offered a cautionary note: the history of AI in medicine includes a 2016 prediction that radiologists would be replaced within four to six years. That did not happen. We have a radiologist shortage. The tools that actually get adopted are not the ones that replace clinical judgment but the ones that extend clinical capacity — Open Evidence, ambient documentation, digital pathology assistance — because clinicians pull these tools toward themselves rather than having them pushed from above.

---

## Theme 4: The Data Infrastructure Challenge

A recurring practical theme across the summit is that AI in oncology is only as good as the data it runs on, and the data infrastructure of most healthcare institutions is deeply fragmented, unstructured, and siloed.

Abernethy identified this as perhaps the most important near-term bottleneck. Most clinically valuable data lives in PDFs and unstructured notes — "digital paper." LLMs and specialized ML models that convert this unstructured text into structured, analyzable data are rapidly improving, and their output creates a virtuous loop: high-quality structured data enables better AI models, which produce better structured data. This transition from unstructured to structured clinical data at scale could unlock training datasets large enough to capture the clinical nuances (the date of the daughter's wedding, the three-and-a-half-hour commute) that currently require a human clinician's intuition.

Gordan noted that data fragmentation across EHRs and labs is one of the central practical barriers to AI deployment in community oncology. FHIR and HL7 integration standards exist but are inconsistently implemented. Prior authorization systems are an especially egregious example of how the absence of interoperability wastes clinician time and degrades care.

Costa described Natera's approach: building a structured, AI-ready "data commons" by processing all commercial testing outputs (whole exome sequencing, RNA sequencing, digital pathology, EMR data, clinical outcomes) into a single formatted data lake. This kind of proprietary, purpose-built data infrastructure — built through commercial diagnostic operations rather than research grants — is presented as a durable competitive advantage.

Abernethy's Highlander Health argument is structurally similar: longitudinal data assets are the infrastructure on which future clinical trials will be nested. The acquisition of Target RWE was driven by the conviction that whoever holds the longitudinal data infrastructure will shape the next generation of evidence generation in medicine.

---

## Theme 5: AI and the Future of Clinical Trials

Multiple speakers pointed to clinical trial acceleration as one of the highest-value applications of AI in oncology — and one where the current system is most broken.

The problem Abernethy identified: clinical trials take six to seven years. Endpoints for long-lived diseases take too long to read out. Documentation requirements are enormous. Patient matching is inefficient. Study designs are rigid. These structural inefficiencies slow the translation of promising treatments into clinical use.

The AI-enabled solutions she described for Highlander Health include: AI-assisted patient matching and recruitment, AI-reduced documentation burden, seamless phase I–III trial designs, 24-hour protocol amendments, and most fundamentally, nested clinical trials embedded in longitudinal data infrastructures — where the data collection that happens as part of normal oncological care simultaneously serves as the foundation for prospective trials.

Gordan added the community oncology perspective on clinical trial matching: tools from Mayo Clinic, Memorial Sloan Kettering, and others have shown 80–96% accuracy in matching patients to trials, reducing screening time from ~110 minutes to ~24 minutes. FCS is actively deploying AI-based trial matching and reporting early improvements in accrual. The goal is to move from single-digit accrual rates toward rates that reflect the genuine eligibility of community oncology patients.

O'Donnell contextualized the stakes: the trials she wants to see are not just detection trials but interception trials — studies that test therapeutic vaccines, fixed-duration immunotherapy, or CAR-T cells in patients identified at the molecular level to have early disease. Detection without interception is incomplete. And those trials can only be designed, enrolled, and read out efficiently with the kind of AI-enabled infrastructure multiple speakers described.

---

## Theme 6: AI in Academic Publishing — Integrity, Transparency, and Speed

The conversation between Flora and Kohane (informatics and publishing) addressed a challenge largely absent from the other sessions but of fundamental importance: what happens to the academic record when LLMs can generate, polish, and potentially fabricate scientific content at scale?

Kohane reported that at least 13% of indexed abstracts show evidence of LLM processing, a major journal recently retracted 129 articles due to undisclosed LLM use, and an estimated 20–25% of peer reviews are AI-assisted. The word "delve" appeared at 28 times its previous frequency in biomedical literature after 2022 — a reliable stylometric marker of LLM-generated prose.

The positions both editors take: disclosure is necessary; accountability rests with human authors, not AI tools; and the use of AI to improve prose (particularly for non-native English speakers) is not only acceptable but equity-promoting. The ethical line is crossed when AI is used to make weak science look stronger, to manufacture data, or to generate reviews or papers without genuine human scientific oversight.

Kohane's *NEJM AI* pilot of AI-assisted peer review — two randomized controlled trials reviewed simultaneously by one human editor and two AI systems, with all reviews published transparently as supplementary material — offers a constructive model. Both AI reviewers performed well: they made no factual errors, focused on different complementary aspects (statistical methodology; generalizability), and agreed with the human reviewer's overall recommendation. Published reviews from both AI systems are available for inspection.

The summit's broader implication is that AI is simultaneously improving and threatening the scientific infrastructure on which evidence-based medicine depends. Maintaining the integrity of the clinical literature requires proactive institutional responses — disclosure requirements, human oversight, performance monitoring — not passive hope that bad actors won't abuse the tools.

Kohane's deeper concern, the "human values project," is that as AI becomes embedded in healthcare's commercial infrastructure, every stakeholder in the system — hospitals, payers, pharma companies, tech vendors — will attempt to tune AI models to serve their financial interests, potentially at patients' expense. Identifying and auditing the values embedded in clinical AI systems is, he argues, one of the most important unsolved problems in the field.

---

## Theme 7: Equity — Who Benefits?

Equity was not the explicit focus of any single session, but it surfaced as a concern in almost every conversation, and its presence across the summit reflects a genuine disciplinary awareness.

Lehman (breast cancer) made the strongest equity argument: traditional clinical risk models for breast cancer screening were built on predominantly European datasets and systematically underestimate risk in Black, Hispanic, and other non-European populations. Clarity deliberately trained on mammograms from women around the world. She also highlighted that younger women — a growing group with late-stage breast cancer diagnoses — are being failed by age-based screening guidelines. AI risk scoring is the tool that makes individual risk-based screening feasible without requiring universal screening of all young women.

Gordan (community oncology) noted that community oncology serves the most geographically and demographically diverse cancer patient population in the country, including underserved and rural patients. AI tools that reduce burnout, improve biomarker capture, accelerate clinical trial matching, and reduce administrative burden all disproportionately benefit settings — community practices, rural hospitals — that have the least slack in their systems.

O'Donnell (cancer screening) noted that the PROMISE study specifically recruits African-American patients and patients with family history, recognizing that standard screening guidelines leave high-risk populations without adequate tools. The broader equity argument for MCED tests: most of the 70% of cancers that lack screening tests disproportionately affect populations already underserved by early detection programs.

Penberthy (2030 vision) mapped cancer incidence and mortality geographically, highlighting mid-America and Appalachia as regions with both high need and inadequate access to advanced cancer care. His vision of the consumer-centric 2030 healthcare model is explicitly one in which the system comes to patients rather than requiring patients to navigate complex institutional access barriers.

The summit's collective position is that AI, properly deployed, is a force for equity — extending the reach of expertise to settings and populations that currently lack it. But poorly deployed, AI can entrench existing disparities if training data is unrepresentative or if the benefits of AI-driven tools flow primarily to well-resourced institutions.

---

## Theme 8: Trust, Governance, and the Human in the Loop

Across the summit, the word "trust" appeared with striking frequency — in Abernethy's framing ("trust is the glue that holds it all together"), in Kohane's analysis of clinical AI adoption, in Gordan's description of AI governance at FCS, and in the closing remarks of multiple speakers.

The consensus view on governance is pragmatic rather than philosophical. Gordan described FCS's standing legal/IT/clinical AI oversight committee, human-in-the-loop verification to prevent automation bias, and explicit FHIR integration standards as the practical apparatus of responsible deployment. Abernethy described the need for performance monitoring infrastructure — the "cockpit" that tracks algorithm behavior over time and signals when retraining or rollback is needed. Kohane and Flora discussed disclosure requirements and human editorial oversight as the governance tools for publishing integrity.

The summit's implicit position on the pace of AI adoption is that skepticism is a feature, not a bug, of a mature clinical culture — but that skepticism must be informed and calibrated, not reflexive. The oncologists who are most circumspect about AI are not wrong to want evidence; the point is to generate the evidence, not to avoid the tools while the evidence matures.

Penberthy closed the day with the most expansive framing: the question of AI governance in medicine is structurally analogous to the transition from horse-drawn carriages to automobiles. The editorials in the 1900 New York Times warning about dangerous flammable vehicles moving faster than seven miles per hour did not stop the automobile; neither will cautionary editorials stop clinical AI. The productive question is not whether to deploy these tools but how to deploy them wisely, with humans accountable for outcomes and systems designed to learn from errors.

---

## Overall Synthesis: The Summit's Collective Argument

The State of AI in Precision Oncology 2025 summit advanced a coherent collective argument that can be stated simply: the tools now exist to fundamentally transform cancer medicine from a reactive discipline that diagnoses and treats advanced disease into a proactive one that detects, intercepts, and prevents cancer across its full biological lifecycle — and AI is the enabling technology that makes this transformation possible at scale.

The evidence base for this argument runs from the molecular (ctDNA at 10⁻⁶ sensitivity, neoantigen prediction, protein structure modeling) through the clinical (ambient documentation, biomarker auto-mapping, trial matching, toxicity prediction) to the systemic (clinical trial acceleration, longitudinal data infrastructure, consumer-facing digital health). It encompasses individual patients (digital twins, MRD-guided therapy) and populations (MCED screening, polygenic risk scores, precision risk-based mammography).

The obstacles are real: data fragmentation, regulatory lag, workforce constraints, reimbursement inertia, and the ever-present risk that commercial interests will shape AI systems in ways that do not serve patients. But the speakers at this summit — practitioners, researchers, editors, and investors who collectively span the entire healthcare ecosystem — are broadly aligned on the direction of travel and on what "going right" looks like: more cancers caught earlier, more patients cured, more clinicians able to bring their full human presence to the work that matters most, and a scientific record that remains trustworthy enough to guide the next generation of discoveries.

---

## Future Directions Identified Across the Summit

Across all sessions, speakers identified the following as the most important priorities for the next three to five years:

**Clinical evidence generation:** Readout of MCED trials (NHS study and others); prospective validation of MRD-guided therapy de-escalation; interception trials testing therapeutic vaccines and fixed-duration immunotherapy in molecularly detected early disease; validation of AI risk scoring in diverse populations.

**Infrastructure:** Widespread FHIR/HL7 interoperability; structured clinical data extraction from unstructured EHR notes at scale; longitudinal data registries as clinical trial substrates; performance monitoring systems for deployed AI.

**Policy and reimbursement:** FDA approval pathways for MCED tests; MCED Act reimbursement legislation (Nancy Gardner Sewell Act); regulatory frameworks for AI-assisted peer review and clinical decision support; transparency requirements for AI systems used in clinical and administrative decisions.

**Equity:** Diverse training datasets; community oncology AI tool deployment; equity-focused MCED studies in high-risk populations; integration of polygenic risk scores to improve risk stratification across ancestry groups.

**AI safety and governance:** Development and adoption of AI disclosure standards in academic publishing; clinical AI performance monitoring infrastructure; research into the values embedded in commercial healthcare AI systems.
