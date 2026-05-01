# Fireside Chat: State of AI in Community Oncology

**Summit:** State of AI in Precision Oncology 2025

**Speaker:**
- **Lucio Gordan, MD** — President & Managing Physician, Florida Cancer Specialists & Research Institute; board member of COA, CODA Executive Board, FLASCO

**Moderator:** Doug Flora, MD

---

## Overview

Dr. Lucio Gordan offers a data-rich, practitioner-grounded survey of how AI is already transforming — and will continue to transform — community oncology in the United States. Community oncology is the setting in which 55–70% of all systemic cancer care is delivered, making it the largest and most consequential context for any nationwide AI deployment in oncology. Gordan covers at least ten distinct domains of AI application, from ambient documentation and treatment safety to biomarker-driven therapy selection and clinical trial matching, backing each with published evidence and illustrating the current state with examples from Florida Cancer Specialists (FCS), one of the country's largest oncology practices.

---

## The Community Oncology Landscape and Its Challenges

Community oncology is characterized by lean staffing, a broad patient mix (most community oncologists remain generalists), financial and regulatory pressures, and a growing mismatch between patient volume and provider supply. Key figures that frame the problem:

- ~60% of U.S. cancer patients are treated in community settings by ~14,000 oncologists
- Burnout affects ~50% of oncologists; the physician shortage is worsening
- Manual EHR data entry, prior authorization, and value-based care reporting (EOM, MIPS, commercial VBCs) collectively consume 20–30% of a physician's working hours
- Data remains fragmented across EHRs and labs, complicating analytics and decision-making

Gordan is clear: AI will not replace physicians, nurses, or pharmacists — the human-to-human interaction is irreplaceable. But AI as a force multiplier, handling the cognitive and administrative overhead that doesn't require that human connection, is already arriving and badly needed.

---

## Domain 1: Ambient AI Documentation

Ambient documentation — AI tools that listen to patient encounters and auto-draft clinical notes — is perhaps the most immediately impactful AI deployment in community oncology. Data cited by Gordan:

- Note time reduced from ~18 minutes to ~10 minutes (and in his personal experience, even more dramatically)
- 45% reduction in after-hours charting ("pajama time")
- Biomarker field completeness improved from 62% to 91%
- 4 hours of EHR time saved per provider per week

The last point has a meaningful downstream effect: higher biomarker completeness directly improves the odds of patients receiving biomarker-driven targeted therapy and being matched to appropriate clinical trials. Gordan adds an anecdotal metric that resonates: a colleague's wife called to say she was having dinner with her husband more often since the AI scribe was deployed.

---

## Domain 2: Treatment Selection and Patient Safety

Community oncology delivers 80–90% of all infusion therapy volume in the U.S. AI-based order-checking and real-time safety tools add a layer of verification that goes deeper than existing EHR alerts. Specific evidence:

- **42% reduction in near-miss prescribing errors** (Bazak et al.)
- **AUC of 0.79 for immune toxicity prediction** — well above the 0.65 threshold considered superior to a well-educated human (Kian et al.)
- **70% drop in infusion mismatches** via computer vision verification of barcodes, infusion rates, and pharmacy mixtures (Lee et al.)

Gordan also highlights predictive toxicity modeling: while humans can analyze 5–9 dynamic variables simultaneously in real time, AI models can analyze millions of data points to anticipate toxicity from lab and clinical data. He describes this as a future where clinicians will use AI-generated risk flags to give extra attention to high-risk patients earlier, preventing avoidable hospitalizations and adverse events.

---

## Domain 3: Physician Wellbeing and Work-Life Balance

Multiple multi-site studies from Mass General, Emory, and others show:
- ~20–30% reduction in burnout among users of oncology-specific AI scribes
- ~30% improvement in documentation-related wellbeing
- Almost universal positive response among providers who use ambient AI

Gordan extends this to the near future: AI-based NLP triage for portal messages (handling the flood of patient-generated communications), LLM-drafted responses for routine prior authorization letters, and automated inbox management. One estimate cited: 40% reduction in inbox real-time load, 25% reduction in stress (Miller et al.).

---

## Domain 4: Revenue Cycle and Fiscal Sustainability

"If we can't pay the light bills, we can't infuse chemotherapy," Gordan says bluntly. AI tools for coding accuracy and billing have shown:

- 20–25% decrease in claim denials
- 3–7% revenue increase — an enormous figure at the scale of a large practice
- 5–10% per month reduction in denials via ML-assisted audits and robotic process automation

These are existential figures for independent community practices under financial pressure.

---

## Domain 5: Biomarker-Driven Therapy and NGS Auto-Mapping

This is an area Gordan describes as one of his greatest passions. There are now over 300 biomarker-linked FDA-approved therapy indications, growing every week. No physician can manually track all of them. FCS is already using AI to auto-map next-generation sequencing (NGS) results to NCCN guidelines, dramatically reducing the cognitive burden of biomarker interpretation. Evidence:

- Guideline concordance improved from **71% to 89%**
- Time from biomarker result to drug selection and authorization reduced by **5 days — more than 50%**
- Structured biomarker completeness improved from **60% to 90%**

This has profound downstream effects on appropriate targeted therapy selection and clinical trial eligibility.

---

## Domain 6: Clinical Trial Matching

FCS — the Florida Cancer Specialists and *Research* Institute — is actively working to improve clinical trial accrual rates, which remain stubbornly in the high single digits. AI-based electronic pre-screening of EHR data is beginning to change this by improving the tokenization and matching of patient characteristics (clinical, lab, diagnostic, staging) against trial inclusion/exclusion criteria.

Evidence from the literature:
- **80% improvement in clinical trial matching** (Mayo Clinic Watson study, breast cancer)
- **40% increase in accrual** after 9 months of LLM implementation, followed by a further 27% increase at 12 months
- Screening time reduced from **110 minutes to 24 minutes** per patient
- 98% accuracy; review time down from **20 minutes to 43 seconds** (Memorial Sloan Kettering, lung trials)

Gordan is candid that most of these studies come from single highly-sophisticated centers and academic systems — the challenge of scaling this across community oncology remains real, but he is optimistic that within 5–10 years it will be achievable.

---

## Domain 7: Predictive Outcomes Modeling

AI models predicting near-term clinical events are already performing well above human baselines:

- **AUC 0.83** for predicting 7-day hospitalization using labs, vital signs, and social determinants of health
- **17% decrease in ER visits**
- **AUC 0.78** for GI toxicity prediction (Aurora et al.)
- **AUC 0.80–0.95** across multiple outcome models — approaching near-perfect predictability
- CAR-T toxicity (ICANS) predicted **5 days before clinical presentation** — a potentially life-saving lead time

These models will increasingly allow oncology teams to be proactive — flagging high-risk patients for earlier intervention rather than responding to crises.

---

## Domain 8: Radiation Oncology AI

While not Gordan's primary domain, he notes the evidence for AI in radiation planning is substantial: improved radiomics and doseomics modeling, better treatment protocol mapping, and predictive models for pneumonitis and other toxicities from radiation combined with immune checkpoint inhibitors.

---

## Domain 9: Immunotherapy Adverse Event Detection

e-PROs (electronic patient-reported outcomes) combined with NLP and machine learning are detecting immune-related adverse events earlier than clinicians can, enabling faster response (dose reduction, corticosteroids, clinical assessment) before toxicity escalates.

---

## Domain 10: Value-Based Care and Administrative Compliance

AI bots for auto-abstracting endpoints for MIPS, EOM metrics, and commercial VBCs are improving data completeness from ~70% to 93% and reducing the time physicians spend on compliance documentation. NLP pipelines extracting diagnosis and AJCC staging from pathology reports show improvement from ~55% to ~95% accuracy.

---

## Governance, Ethics, and AI Oversight

Gordan emphasizes that none of this works without robust governance. FCS maintains a standing legal/IT/clinical oversight committee that meets regularly to review AI deployments, set boundaries, and ensure explainability and privacy. Key principles:

- **Human-in-the-loop** verification to prevent automation bias
- **FHIR and HL7 integration** to ensure data flows correctly between systems
- Alignment with privacy and ethics frameworks before deployment

He flags prior authorization reform as a critical area where better FHIR API integration between payers and providers could dramatically reduce one of the most universally hated administrative burdens in oncology.

---

## Conclusions and Call to Action

Gordan closes with a direct message to his audience: AI literacy is not optional. He encourages every physician leader and practice administrator to spend 15 minutes per day learning about AI — reading an article, testing a tool, following the literature. "AI is like learning a new language," he says, echoing Doug Flora's advice that daily engagement is the path to competency.

His summary vision: AI will deliver fairer cancer access, redefine efficiency and precision in community oncology, and — when implemented responsibly — allow more patients to get the right therapy sooner, experience less toxicity, and participate in clinical research that further improves outcomes for everyone.
