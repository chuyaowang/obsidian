# Multiomics Data Management

**Speaker:** Chris Dwan  
**Affiliation:** Independent consultant; former Research Computing Lead, Broad Institute; former CIO, Semaphore (now GeneDx); founder of early bio-IT consulting at The BioTeam  
**Event:** State of Multi-omics and NGS 2026 Summit (GEN / Illumina)  
**Host:** Kevin Davis, GEN Editorial Director  

---

## Background

Managing biological data has always involved balancing scientific relevance, technical scalability, and organizational discipline. As genomic and multiomics technologies have advanced — from early-2000s computational biology to petabyte-scale cloud genomics — the challenges of managing data have shifted from storage hardware to human organization, from file naming to data governance, and from individual lab conventions to cross-disciplinary alignment.

**TCGA (The Cancer Genome Atlas)** is the paradigmatic large-scale genomics data project: a 12-year initiative collecting samples from 11,000 cancer patients across 33 tumor types at ~20 collaborating institutions. It established a canonical **four-level data classification** that remains the field's best-practice framework for managing biological data:

- **Level 1:** Raw instrument output (e.g., FASTQs, raw mass spec images)
- **Level 2:** Normalized and quality-controlled data (e.g., BAM files) — the key archival level; transformed but not discarded
- **Level 3:** Derived biological statements (e.g., variant calls relative to a reference genome) — interpretations, not direct measurements
- **Level 4:** Clinical or biological interpretations (e.g., pathogenic variant classifications) — inferences with the highest added value and the most assumptions embedded

Understanding which level of data one is working with is essential for reproducibility, cross-modal integration, and appropriate use of downstream computational tools.

The emergence of **AI and large language models** has added a new category of data-like artifacts — model outputs, imputations, synthetic completions — that do not fit cleanly into any TCGA level. A key conceptual distinction Dwan develops throughout is that AI outputs are not observations of the world and must be treated differently from primary data.

---

## Section 1: Framing the Problem — Domain Expertise as the Core Asset

Dwan opened with two epigrams that frame his entire argument:

A bioinformatician from the University of Minnesota (over 20 years ago): *"Bioinformatics is full of pitfalls for those who look for patterns or make predictions without a thorough understanding of where biological data come from and what they mean."*

Donald Knuth (computer science's founding figure): *"People who are more than casually interested in computers should have some idea of what the underlying hardware is like. Otherwise, the programs they write will be pretty weird."*

Both quotes make the same claim: **you must understand where your data come from** to use them correctly. Dwan argued this principle is more important today than ever, because the gap between generating data and understanding its origins is widening. AI tools can process data at unprecedented speed, but they cannot substitute for the biological and technical knowledge required to interpret what the data mean and where they might be wrong.

Dwan's career trajectory illustrated this principle: starting with AI/neural networks in the 1990s (missile targeting for a military contractor, where "nothing worked"), pivoting to computational genomics after realizing he knew nothing about biology, spending years sitting with postdocs and attending introductory courses, then building HPC infrastructure at institutions ranging from NASA and the New York Genome Center to the Broad Institute and Semaphore. At every stage, the limiting factor was not computation but the human expertise required to ask sensible questions of the data.

---

## Section 2: Data — What It Is and What It Is Not

Dwan used the TCGA four-level framework to make a critical point about the current landscape: **AI outputs sit outside this framework entirely**.

Level 2 (normalized primary data) is the canonical archival target: it represents the instrument's actual observations, transformed but with no information discarded. For sequencing, this means BAM files; for mass spectrometry, the raw spectral images. This is the data that is reproducible in the strictest sense. Level 3 introduces interpretation (variants called against a reference genome are not directly measured — the reference genome is itself a construct full of complexity). Level 4 is clinical reasoning on top of that.

AI-generated synthetic data, imputations, and model completions are **none of these things**. They are useful tools, but they are not observations of the world. Dwan flagged a recent headline claiming that AI could "generate data faster than we can measure it in the lab" as a dangerous conflation: synthetic data and AI outputs can be valuable for training and hypothesis generation, but treating them as primary data in a scientific archive risks systematically corrupting the knowledge base on which future models will be built.

He recommended consulting a statistician for anyone tempted to treat synthetic data as equivalent to empirical observations.

---

## Section 3: Data Management Best Practices

Dwan gave practical, opinionated guidance for organizations at different scales:

**Starting out:** Just use the cloud. The economics and operational overhead of purchasing, maintaining, and cooling physical hardware are unjustified until reaching ~100 terabytes. At that scale, begin evaluating the economics of renting versus owning.

**What to archive:** Archive Level 2 — the normalized, quality-controlled version that has not yet undergone any lossy transform. For sequencing this means BAM files; for mass spec, the raw images. Do not keep off-instrument files, multiple intermediate formats, and BAMs all separately: the intermediate formats are usually the same data and the largest files.

**Indexing:** Archive and index in **sample space**, not instrument space. The downstream user needs to find data by biological entity (sample, patient, tissue type, experimental condition), not by which flow cell or instrument run produced it. "What happens in the lab should stay in the lab" — instrument metadata is important to retain but should not be the primary access key.

**Naming conventions:** Descriptive file names are always necessary because humans need to navigate the pile. Strike a balance: overly rigid conventions delay data capture and fail when the science changes; overly loose naming creates chaos. The maxim is to never let perfect be the enemy of good — catch data first, clean up later. A **NoSQL database** (indexed against the file system) plus a **visual dashboard** (achievable in a couple of days with modern AI-assisted coding tools) is the practical upgrade path from a flat file system.

Dwan cited Mike Noble's dashboard at Breakthrough Cancer as an example: indexing ~1 million files with visual cross-tabulation that lets the team subset by project, sample type, and data level with a few clicks. He emphasized that any dashboard must include **checksums** — numbers that should be consistent when summed horizontally and vertically — to catch silent data corruption or accounting errors.

**Build for flexibility:** Dwan shared the example of Ben Yuenkampen's January 2026 paper describing a newly discovered cell type in Drosophila that replicates DNA without undergoing mitosis or meiosis, simply growing in ploidy over the organism's lifespan. No data model he has ever built would have accommodated this finding. Data architectures must be designed to handle surprises, because biology keeps producing them.

---

## Section 4: Data Management as an Organizational Problem

"At scale, all problems become people problems." Dwan devoted significant time to the organizational and human dimensions of data management, arguing that technology alone cannot solve them.

He proposed the concept of a **Data Czar** (alternatively, Data Steward — but with genuine authority, not a "data janitor"). This person's role is to:
- Engage with the scientific community across all disciplines, not only genomics
- Write alerting, automation, backups, and dashboards that make scientists' lives easier
- Identify and surface problems that are answerable with numbers, so the team can focus on questions about what to do next
- Advocate for appropriate investment in data infrastructure by framing data assets as having capital value

Dwan made the point that if organizational leadership cannot answer "what is the capital value of our data assets?", then investment in those assets will remain underfunded. Data is treated as invaluable in abstract but poorly resourced in practice. Framing the question concretely drives appropriate hiring and tooling decisions.

The **CIO/IT leadership** role is risk management and cost containment — not obstruction, but setting safe speeds. Dwan used the metaphor of a high-performance race car: it can go very fast precisely because it has excellent brakes. Information security is the brakes; without them, no sensible person would drive the car at full speed.

---

## Section 5: Information Security in the AI Era

Dwan argued that **security by obscurity died approximately in 2025**. The practices historically tolerated — informal assumptions that "there's no HIPAA data here," clinical data on SharePoint, unvetted API integrations — are no longer defensible when AI agents can autonomously probe every permission boundary and exploit every misconfiguration.

He referenced Anthropic's new model (referred to as "Maven" — likely a pseudonym or fictional name used in the talk) reportedly finding major zero-day vulnerabilities across multiple operating systems, illustrating the accelerating capability of AI as both a security tool and a security risk.

He proposed a three-category framework for data sensitivity:
1. **Regulated data:** Data required for FDA, SEC, or patent filings — provenance and chain of custody are critical; errors here can invalidate drug approvals, patents, or IPOs.
2. **Restricted data:** Personal and private data (medical records, employment, banking) — breach causes direct harm to individuals and regulatory penalties.
3. **Confidential data:** Competitively valuable data chosen to be private (drug candidates, protein sequences, source code, prompts). Prompts are now code: if they leak, so does competitive advantage.

The critical message to team members: "We cannot just say no anymore because the tools are too powerful." Access restrictions that are unrealistically strict will be routed around by users, creating shadow data stores and untracked AI integrations — which is worse than a controlled, well-governed AI adoption. Organizations need to review AI vendor terms and conditions and develop realistic acceptable-use policies.

---

## Section 6: Multi-omics — The Multidisciplinary Synthesis

Dwan used a Star Trek metaphor to describe multi-omics: combining different ships, captains, aliens, and series, each with partial and imperfect mappings to one another. The point is that multi-omics is not merely more data; it is the **collision of different scientific disciplines**, each with its own vocabulary, ontology, data types, and assumptions.

Language and metadata standards become critical when integrating data across modalities — the suffix conventions (genomics = study of the genome; transcriptomics = study of all transcripts; metabolomics = study of all metabolites; multi-omics = integration of all these) are useful while they serve communication but become counterproductive when they obscure what is actually being measured or when they are applied promiscuously to imply a depth of integration that doesn't yet exist.

He quoted John Quackenbush (whose lab has been in the news for relocating due to federal research policy changes): "Every revolution in science, from the Copernican heliocentric model to the theory of the gene, has been driven by one and only one thing — access to data." Dwan endorsed this view but added the corollary: access must be paired with appropriate context, curation, and expertise to avoid producing confusion rather than insight.

On the **natural language interface** revolution: the turning point in Dwan's understanding came from a conversation with a Chief Medical Officer who wanted statistics from structured patient records. The CDO and Dwan suggested SQL; the CMO replied: "I don't know SQL and I'm not going to learn. I want to do this without asking your permission." That statement captures the transformative power of LLM-mediated data access: it democratizes interaction with data across disciplines, eliminating the technical bottleneck. But it does not grant domain expertise, and the early-stage turbulence of non-experts drawing potentially incorrect conclusions from correctly executed queries is a real organizational risk that will require active management.

---

## Q&A Highlights

**Q: What are clients most often asking about right now?**  
The dominant question is: "What is the appropriate level of aggression with which to engage with AI?" Dwan's consistent advice is to refocus on mission: technology is *how* you do something, not *what* you're doing or *why*. The risk is that organizations optimize for adopting new tools rather than for the scientific or clinical outcomes those tools are supposed to serve.

**Q: Can you version and characterize AI outputs?**  
Technically yes, but without reliable reproducibility: the same prompts and input may not reliably produce the same output across model versions. The practical solution is ruthlessness about discarding intermediate AI outputs rather than archiving everything. Good scientists already have versioning discipline for pipelines; that discipline needs to extend to AI-generated intermediates.

**Q: Which data level is most useful for training AI models in genomics?**  
Models that actually work are those confined to a narrow, well-curated slice of biology with clean, well-organized data. The principle is to process data to the level necessary for the question being asked, and no further. Don't ask a neural network to rediscover codon usage tables from raw reads; precompute what you know.

**Q: Should dashboards serve real-time QC or periodic static updates?**  
Both. A well-maintained dashboard is a living system, continuously updated. With modern AI-assisted coding tools, an MVP is achievable over a weekend. The goal is to preemptively answer questions that are answerable by numbers, freeing the team to focus on questions about what to do next.

**Q: How do you handle the intrinsically disordered regions of the genome?**  
These regions were once called "dark matter of the genome." We can observe functional consequences (expression effects, methylation-linked regulation, non-germline heritable effects) but lack a strong representational vocabulary for their sequence-level function. This remains primarily an open biology question rather than a data management problem per se.

**Q: How do you convert descriptive file names to consistent structured metadata without doing it manually?**  
You can't fully automate this: there is no way to infer what a laboratorian did from file names alone without having the conversation. Dates can be normalized programmatically, but metadata reflecting experimental decisions requires direct engagement with the scientists. Once a transformation is performed two or three times, it should become a script.

**Q: How does data science advance multi-omics integration?**  
By taking **cross-cutting perspectives** that transcend the disciplinary silos in which data are generated. Most biological systems break not within the domain of a single team but at the boundaries between domains — genomics and proteomics, clinical and molecular, time and space. Data science's contribution is to look at those seams and ask whether the disciplinary categorizations are actually the most useful ways to organize knowledge about the system.

---

## Summary

Chris Dwan delivered a practitioner's perspective on multiomics data management that deliberately avoided AI hype in favor of durable organizational and technical principles. His argument proceeds in three nested layers: first, that domain expertise — knowing where data come from and what they mean — is the irreducible prerequisite for sensible data management; second, that data management requires a responsible human actor (the Data Czar) with cross-cutting authority and a mandate to serve the scientists; and third, that multi-omics is fundamentally a multidisciplinary problem that will break at disciplinary boundaries unless those boundaries are actively managed.

The TCGA four-level data classification framework provides the conceptual backbone: archive Level 2 (normalized primary data), be cautious about Level 3 and 4 (interpretations and inferences), and recognize that AI outputs belong to none of these categories and require separate treatment. The democratizing power of natural language interfaces to data is real and transformative, but it accelerates access without guaranteeing understanding — a risk that organizations must manage explicitly rather than assuming AI will sort it out. The talk's most enduring message is a quiet one: the people who are quiet and diligent and thinking deeply will have sustained insights. Those who are loudest and most confident are probably trying to sell something.
