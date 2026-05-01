# Adventures in AI, Informatics and Publishing

**Summit:** State of AI in Precision Oncology 2025

**Speakers:**
- **Doug Flora, MD** — Executive Medical Director, Yung Family Cancer Center, St. Elizabeth Healthcare; Editor-in-Chief, *AI in Precision Oncology (AIPO)*
- **Isaac (Zak) Kohane, MD, PhD** — Chair, Department of Biomedical Informatics, Harvard Medical School; Editor-in-Chief, *NEJM AI*

---

> **Relevant Links & References:**
> - [TensorBlack: Clinical AI Talks](https://tensorblack.ai/) — a resource for clinical AI content referenced in the summit
> - **Book by Isaac Kohane:** *The AI Revolution in Medicine: GPT-4 and Beyond* (co-authored with Carey Goldberg and Peter Lee) — a book Flora describes as foundational reading and which Kohane discusses at length during the conversation

---

## Overview

This fireside chat brings together two physician-editors at the forefront of AI-driven academic publishing in medicine. Kohane, a pediatric endocrinologist with a PhD in computer science from the 1980s, is founding editor of *NEJM AI* — the first AI-focused journal from the prestigious New England Journal of Medicine group. Flora, as editor of *AIPO*, leads a newer publication in the oncology AI space. Their conversation explores three intertwined themes: the use of AI in medical research and clinical practice, the ethical and integrity challenges that LLMs pose for academic publishing, and the potential for AI to both accelerate and corrupt the scientific record. The exchange is marked by deep mutual respect and honest candor about the field's most uncomfortable tensions.

---

## The Origin Story of NEJM AI

Kohane recounts being approached by Jeff Drazen and Eric Rubin (successive editors-in-chief of NEJM) six or seven years ago to start an AI journal. He initially refused — he felt there wasn't yet enough high-quality, clinician-relevant AI research to sustain a serious journal. By 2020 he reconsidered. Then, in October 2022 — before GPT was public knowledge — he received a call from Peter Lee, head of Microsoft Research, who introduced him (under strict secrecy) to GPT-4, then codenamed Da Vinci-3.

What struck Kohane immediately was not just its capabilities but its early disposition: the model argued with him about diagnoses in "an impertinent way, which I actually enjoyed." He found it less obsequiously aligned than current versions. He immediately saw the clinical potential, invited the NEJM editors to a demonstration, and they saw the future. The journal launched at almost exactly the moment that GPT-3.5/ChatGPT exploded into public consciousness — giving it immediate relevance and an audience. By early 2023, smart clinicians were already using GPT to write prior authorization letters to insurers.

---

## Science Fiction as a Lens for AI in Medicine

The conversation opens with Flora's reference to Chapter 10 of Kohane's book, which uses the 1950 C.M. Kornbluth science fiction story *The Little Black Bag* as a central metaphor. The story follows an alcoholic, incompetent physician who receives a bag of medical devices from the future and, with these tools, is suddenly able to cure patients effectively. The lesson Flora draws: even when given extraordinary tools from the future, the human character of the wielder determines the outcome. The tools were eventually compromised by the physician's greedy partner, who exploited them for personal gain — and came to a bad end.

Kohane extends the science fiction theme, noting his lifelong reading habit and the surprising utility of the genre for the current moment. He describes Susan Calvin from Isaac Asimov's *I, Robot* series as a "robo-psychologist" who debugs robots by interrogating them as a psychologist — because the robots are too complex to analyze at the circuit level, just as GPT models are too complex to analyze at the neuron level. The primary mode of understanding modern AI is behavioral and conversational, not mechanistic — a direct parallel.

He also alludes to the "Marching Morons" trope in science fiction — the fear of human de-skilling as AI handles more cognitive tasks. Both Flora and Kohane take this seriously: they both edit journals precisely because they want to disseminate knowledge and resist intellectual complacency.

---

## AI Adoption in Clinical Medicine: What's Actually Happening

Kohane offers a pointed observation about the pattern of AI adoption in medicine:

Clinical AI tools that received intense academic attention from around 2018 onward — convolutional neural networks for dermatology, radiology, and pathology — are still not widely used in clinical practice, years later. The adoption has been slow.

By contrast, ambient dictation tools and *Open Evidence* — an LLM trained on biomedical literature, partnered with NEJM, NCCN, and JAMA, available free to clinicians — have been adopted almost overnight. Open Evidence, now a $6 billion–valued company, is used by tens of thousands of clinicians daily, often without hospital approval or oversight. Clinicians know it sometimes hallucinates, yet find it so practically useful they keep using it.

Kohane interprets this pattern as revealing the underlying motivations of both health systems and clinicians. Systems are willing to pay for tools that improve billing and reduce administrative load. Clinicians are willing to adopt tools that reduce cognitive friction in the moment — even without formal validation — if they demonstrably help with the questions they face every day. Radiology and pathology AI, by contrast, requires integration into institutional workflows and raises questions of liability and autonomy, slowing adoption.

> **Note:** [Open Evidence AI](https://www.openevidence.com/) — referenced by both speakers as a rapidly adopted clinical AI tool.

Kohane singles out oncology as the clinical area where AI adoption in clinical contexts is furthest ahead, attributing this to the stakes of the decisions, the culture of knowledge management (NCCN guidelines are uniquely detailed), and the comfort of oncologists with complex, probabilistic reasoning.

---

## The Academic Publishing Crisis: LLMs and Integrity

Flora pivots to the publishing integrity challenge, noting that:
- At least 13% of abstracts indexed in major databases show evidence of LLM processing or contribution
- A major journal recently had to retract **129 articles** from a single publication due to undisclosed LLM use
- The word "delve" appeared at 28 times its previous frequency in the biomedical literature after 2022 — a reliable telltale of LLM-generated prose, along with "tapestry," "beacon," "showcasing," and other characteristic vocabulary

Both editors also note that an estimated 20–25% of peer reviews are now AI-assisted, again frequently undisclosed.

**NEJM AI's policy on authorship and disclosure:**
When the journal was founded, *Science* editor Holden Thorpe initially banned all AI use by authors. Kohane's editorial board — populated with AI researchers — pushed back. Their position: NEJM AI is not publishing literature; it is publishing scientific results. The standard is whether authors can stand behind their science, not their prose style. AI use for writing is therefore allowed provided it is disclosed.

Kohane drew a clear ethical line: using AI to improve prose is comparable to using a research assistant or a medical student to help with literature review, and he argues it levels the playing field for non-native English speakers whose science may be excellent but whose writing in "American medicalese" might otherwise be rejected. He disclosed his own AI use — ChatGPT for outlining, Perplexity for historical research — in his book's acknowledgments section.

The blurred line, however, is when AI assistance begins to make weak science look stronger than it actually is, or enables outright fraud. He demonstrated this personally in a Congress of Peer Review talk: he fabricated a plausible-sounding hypothesis (higher H-index authors have more retractions), generated synthetic supporting data with GPT, and then refined the data through multiple iterations until it passed every standard statistical integrity test. The lesson: any motivated actor can now use LLMs to manufacture convincing-looking data.

---

## The AI Review Experiment

One of the most discussed recent initiatives from *NEJM AI* is a pilot program testing AI peer review. After considerable internal deliberation, the editorial board agreed to the most aggressive scenario Kohane proposed:

- The journal identified two high-quality preprints (both randomized controlled trials of ambient dictation tools) and approached the authors with an offer: guaranteed 7-day decision (accept or reject) in exchange for allowing AI reviewers alongside one human reviewer.
- Both author teams accepted.
- One human editor reviewed each paper. Two different AI systems were also given the papers to review independently.
- The AI reviewers made no factual errors. Each AI focused on different aspects: one on statistical methodology, the other on generalizability and external validity.
- All three reviewers — human and both AIs — reached the same overall recommendation.
- The full reviews by the human and both AI systems are published as supplementary material alongside the accepted papers.

Kohane's assessment: "it was damn good." He acknowledges that this is a carefully supervised pilot, and that the risks of fully autonomous AI review at scale — particularly at predatory journals without editorial integrity — are real. He predicts there will be journals that deploy robotic editors and reviewers with no human oversight, generating fast-turnaround publications that contaminate the scientific literature.

---

## The Broader Stakes: Whose Values Are in the AI?

The conversation closes on a theme that Kohane frames as his primary current research focus: **the human values project**. As AI becomes embedded in healthcare's commercial infrastructure — hospital billing systems, insurance reimbursement decisions, clinical decision support tools — every actor in the system (hospitals, payers, pharma, tech companies) has a financial incentive to tune the AI in ways that serve their interests. Some of these tunings will not be in patients' best interests.

Kohane notes that Open Evidence is already serving targeted advertisements to the clinicians who use it. As LLMs become the backbone of clinical decision-making, the risk is not just hallucination or technical error — it is deliberate or inadvertent shaping of clinical recommendations by the financial interests of the companies that deploy them. Understanding what values are embedded in these systems, and how to audit and preserve the patient-centered values we want them to have, is — in his view — one of the most important unsolved problems in AI in medicine.

Flora agrees, drawing the explicit parallel back to *The Little Black Bag*: the tools from the future are in our hands. What destroys the characters in the story is not the tools themselves, but the greed and short-sightedness of the humans wielding them.

---

## Key Themes and Conclusions

**The science fiction future is now.** Tools that seemed speculative a decade ago — models that argue about diagnoses, that write clinical notes, that review papers — are here. The question is whether we will use them wisely.

**Adoption asymmetry is revealing.** The tools doctors have adopted fastest (ambient dictation, Open Evidence) are the ones that reduce immediate cognitive friction. The tools that require institutional change (radiology AI, pathology AI) are lagging despite strong evidence. This tells us something important about where intervention is most needed.

**Publishing integrity is under genuine strain.** LLMs make it dramatically easier to both improve and fabricate scientific output. The response — disclosure, human oversight, faster turnaround with accountability — is better than either banning AI use or ignoring the problem.

**The coming battle is over values, not just accuracy.** As AI becomes integrated into clinical systems owned and operated by commercial actors, the question of whose interests those systems optimize for will become urgent. Physician editors, professional societies, and regulators will all need to be engaged in answering it.
