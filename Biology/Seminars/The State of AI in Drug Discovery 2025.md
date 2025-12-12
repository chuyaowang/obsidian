# The State of AI in Drug Discovery 2025

#seminar 
> GEN symposium

## Democratizing Small Molecule Drug Discovery with Boltz-2

> [Boltz-2 model github](https://github.com/jwohlwend/boltz)
> [Deepwiki Boltz-2](https://deepwiki.com/jwohlwend/boltz)
> [GEN News Boltz-2](https://www.genengnews.com/topics/artificial-intelligence/boltz-2-released-to-democratize-ai-molecular-modeling-for-drug-discovery/)
> [GEN News Boltz-2](https://www.genengnews.com/topics/artificial-intelligence/boltzgen-democratizes-ai-therapeutic-design-expands-druggable-universe/) (Another one)
> [Boltz-gen github](https://github.com/HannesStark/boltzgen): new model released by Boltz
> [Boltz gen deepwiki](https://deepwiki.com/HannesStark/boltzgen)

**Speakers:**
- Gabriele Corso, PhD, MIT Jameel Clinic
- Regina Barzilay, PhD, Distinguished Professor of AI & Health at MIT Jameel Clinic
- Najat Khan, PhD, Chief R&D Officer, Commercial Officer at Recursion
**Coordinator:** Fay Lin, PhD, Senior Editor at GEN

---

### Sectional Summary of the Talk

The discussion unfolds in a logical sequence, starting from the model's origin, explaining its core scientific contribution, detailing its impact, and concluding with future challenges and directions.

#### 1. Origin Story: The Genesis of the BOLTS Series

- **Challenge:** The release of DeepMind's AlphaFold 3 marked a significant advance in predicting a wide spectrum of biomolecular interactions. However, its initial limited availability through a web server, without open-source code, created a barrier for the broader research community to build upon, validate, and utilize the technology.
- **Method & Goal:** As articulated by **Gabriele Corso** and **Regina Barzilay**, the primary motivation was to replicate the state-of-the-art capabilities of AlphaFold 3 in an open-source model. This would democratize access and provide a foundational tool for their lab and others to continue research. Regina Barzilay humorously noted her initial skepticism about the ambitious goal, given the project's scale, but praised the students' ability to deliver BOLTS-1 in record time.
- **Transition:** This successful creation of a powerful, open-source structure prediction model set the stage for tackling an even more complex problem in drug discovery, leading to a pivotal industry partnership.

#### 2. The Partnership with Recursion for BOLTS-2

- **Challenge:** While BOLTS-1 matched AlphaFold 3's structural prediction, the next frontier was predicting **binding affinity**—the strength of a drug-target interaction. This is a critical bottleneck in drug discovery.
- **Method & Goal:** The partnership between MIT and Recursion was formed to develop BOLTS-2. **Najat Khan** explained that the collaboration was a "mission-driven collision" of urgent need and unique capabilities. MIT provided the algorithmic expertise, while Recursion brought its AI research team (Valence), massive compute power (one of the fastest supercomputers in life sciences), and a sharp focus on practical application in its drug discovery pipeline. **Regina Barzilay** added that the personal connection and prior collaborations with Najat Khan helped facilitate the partnership, which was sparked at a Danaher meeting.
- **Transition:** The partnership's focus was clear: leverage the structural foundation of BOLTS-1 to solve the long-standing challenge of binding affinity prediction.

#### 3. The Significance and Challenge of Predicting Binding Affinity

- **Challenge:** **Gabriele Corso** explained that predicting binding affinity is historically difficult for two main reasons:
    1. The training data is sparse and notoriously noisy.
    2. Binding affinity is a property of the entire dynamic distribution of complex structures, not a single static pose.
- **Method & Goal:** The key insight for BOLTS-2 was to leverage the powerful structural understanding that the model (like BOLTS-1 and AlphaFold 3) had already learned from being trained on vast amounts of structural data (PDB). This pre-trained knowledge provided a robust foundation to tackle the noisy and sparse affinity data. **Regina Barzilay** emphasized that a crucial step was the meticulous curation of high-quality data for training and testing, as simply using all available public data produces noisy, unreliable models.
- **Transition:** With a model that could now predict not just the "how" (pose) but the "how well" (affinity) of a drug binding, the conversation shifted to how this capability transforms the real-world drug discovery process.

#### 4. Impact on the Drug Discovery Pipeline

- **Challenge:** Traditional drug discovery involves slow, expensive, and resource-intensive lab work to determine binding affinity. This limits the number of compounds that can be tested, forcing researchers to rely on a biased, "artisanal" selection of what they *think* might work.
- **Results & Impact:** **Najat Khan** described BOLTS-2 as a "true force multiplier." It provides near gold-standard accuracy (approaching physics-based methods like FEP) but at speeds **~1000x faster**. This changes the economics entirely, allowing researchers to go from screening hundreds of compounds experimentally to screening *millions* virtually. This enables a more unbiased, engineering-driven approach.
- **A Key Application (Novel Targets):** Najat highlighted a critical impact area: novel biology. For new, uncharacterized targets, high-quality crystal structures are often unavailable, which is a roadblock for traditional and computational methods. BOLTS-2 can generate high-quality 3D complex structures, which can then be fed into physics-based simulations (an approach Recursion calls BOLTS-ABFE). This "removes the experimental block," encouraging scientists to pursue novel and challenging targets without being deterred by the lack of a crystal structure.
- **Regina Barzilay** added that affinity is also crucial for understanding the fundamental **biology of disease**, as many biological mechanisms are distinguished by varying affinities, not just the strongest possible binding.

#### 5. Open Source, Community Response, and Data

- **Challenge:** How do you balance commercial incentives with open access? And how do you address the persistent data gaps that limit all AI models?
- **Community Response:** **Gabriele Corso** reported over half a million downloads of BOLTS-2, with usage spanning every big pharmaceutical company, small biotechs, and academic labs. The open-source nature created a rapid feedback loop, with the community independently validating the model, identifying where it works well (well-structured proteins) and where it struggles (dynamic proteins, allosteric sites), and even building new models on top of it.
- **The Data Debate:**
  - **Regina Barzilay** argued passionately for the need for more public data generation, urging the federal government to fund these efforts as a communal benefit, similar to how the PDB was created. She noted that while industry collaborations are helpful for feedback, they rarely result in public data due to legal constraints.
  - **Gabriele Corso** offered a "contrarian view," arguing that algorithmic creativity can often bridge data gaps. He pointed out that the data to "solve" protein folding existed for 20 years before AlphaFold 2 was developed, implying that innovation in algorithms is just as, if not more, important than sheer data volume.
  - **Najat Khan** synthesized these views, stating that a company's competitive advantage will not come from the models themselves (which are becoming commoditized) but from three other areas: **1) A deep understanding of novel biology**, **2) The integration of models into end-to-end workflows**, and **3) The generation of high-quality, proprietary data** in areas that are current blind spots.

#### 6. Future Gaps and What's Next for BOLTS

- **Gaps:** The panel identified several key areas for future work:
  - **Translational Science:** Moving beyond binding affinity to predict pharmacokinetics/pharmacodynamics (PK/PD), toxicity, and human dose response. Najat noted this is a huge unlock, as most failure data is never published.
  - **Difficult Protein Classes:** Improving performance on targets that are more dynamic or have flat, challenging binding pockets.
  - **Data Generation:** Creating high-quality, repeatable, and generalizable data through automation to feed the next generation of models.
- **What's Next:** **Gabriele Corso** announced the release of **BOLTS Gen**, a new model that moves from prediction to **design**. It is a protein binder design model capable of designing peptides, nanobodies, and antibodies against virtually any biomolecule. He highlighted that, like with BOLTS-2, they have already collaborated with ~30 partners to experimentally validate its designs across a wide range of targets, including very difficult cases where human chemists had previously failed.

---

### Q&A Session Summary with Contextual Knowledge

**Q1: How is the confidentiality of input data and output work products addressed in Boltz-2?**

- **Contextual Knowledge:** Pharmaceutical companies invest billions in discovering novel drug targets and chemical compounds. This information is their most valuable intellectual property. Using a third-party cloud service where this proprietary data could be logged, stored, or exposed, even accidentally, represents an unacceptable security risk. Therefore, any tool must be usable within a company's own secure, private computing environment.
- **Answer Summary:** **Gabriele Corso** and **Najat Khan** emphasized that because Boltz-2 is fully open-source, companies can download and run it on their own private servers. This keeps all proprietary inputs (like novel targets or compound libraries) and outputs (predicted binders) completely confidential, which has been a key driver of its adoption in the industry.

**Q2: What are recommendations for improving Boltz-2's performance when it doesn't match a researcher's own experimental binding affinity data?**

- **Contextual Knowledge:** An AI model's "out-of-the-box" performance refers to its accuracy on a new task without any task-specific training. Drug discovery is highly specialized; a general model trained on public data may not understand the nuances of a specific protein family or a novel chemical series. "Fine-tuning" is the process of further training the pre-trained model on a smaller, specific dataset (e.g., a company's internal experimental data) to improve its accuracy on that specific task.
- **Answer Summary:** **Gabriele Corso** noted that the model works well out-of-the-box on about 40% of new campaigns, meaning for the other 60%, it needs more work. This involves fine-tuning the model with internal data or adding other conditioning information. **Najat Khan** added that this is where Recursion's "wet lab" automation shines, as they can quickly generate new experimental data to feed back into the model in a rapid iterative learning loop, improving its predictions for that specific project. She also suggested combining Boltz-2 with other physics-based models for a more robust "ensemble" approach.

**Q3: Are there plans to expand the model to other modalities, like covalent ligands?**

- **Contextual Knowledge:** Most drugs are "non-covalent," meaning they bind to their target reversibly through weaker intermolecular forces. "Covalent ligands" are designed to form a strong, permanent chemical (covalent) bond with their target protein. This can lead to greater potency and duration of effect but is harder to design and carries a higher risk of off-target toxicity. Modeling this requires predicting not just a binding pose but a chemical reaction, which is a more complex quantum mechanical problem.
- **Answer Summary:** **Gabriele Corso** confirmed that while the structure prediction part of BOLTS-2 is general, the affinity prediction is currently focused on non-covalent small molecules. They are actively working to expand its applicability, explicitly mentioning that work on protein-protein and protein-antibody affinity prediction is in progress.

**Q4: How can researchers use Boltz-2 to study dynamic molecular mechanisms, since PDB structures are often static?**

- **Contextual Knowledge:** Proteins are not rigid, static objects. They are flexible molecules that constantly move, breathe, and change shape ("conformational dynamics"). These motions are often essential for their biological function and for how a drug binds. Most experimental structures in the Protein Data Bank (PDB) are static snapshots from methods like X-ray crystallography, which don't capture this dynamism. Modeling these dynamics is a classic challenge in computational biology.
- **Answer Summary:** **Gabriele Corso** acknowledged this is a major challenge. BOLTS-2 was trained with some short molecular dynamics (MD) simulations, so it can predict small, local ensembles of movement, but it still struggles to predict large-scale conformational changes. **Najat Khan** added that this is why it's important to have a suite of tools; physics-based methods like QM/MD can be combined with AI models to better capture the dynamic nature of drug binding.

**Q5: How do you reconcile that a less potent binder might be better for PK/PD and therapeutic index during lead optimization?**

- **Contextual Knowledge:** This question gets at the heart of real-world drug development.
  - **Potency (Affinity):** How tightly a drug binds its target. Higher is not always better.
  - **Pharmacokinetics (PK):** What the body does to the drug (Absorption, Distribution, Metabolism, Excretion - ADME). A drug must be absorbed, get to the right place, and not be cleared too quickly.
  - **Pharmacodynamics (PD):** What the drug does to the body (its effect).
  - **Therapeutic Index (TI):** The ratio of the toxic dose to the effective dose. A high TI is crucial for safety.
    A drug can be extremely potent but fail because it's toxic, can't be absorbed, or is metabolized instantly. The goal is **Multi-Parameter Optimization (MPO)**—finding a balanced compound, not necessarily the most potent one.
- **Answer Summary:** **Najat Khan** strongly agreed, stating this is a critical point in lead optimization. The most potent binder is often not the final drug candidate. She explained that approaches like MPO and active learning are essential to find compounds with the best overall balance of properties (potency, PK/PD, safety). The key is to test all these properties in rapid Design-Make-Test-Analyze (DMTA) cycles, which is where automation in chemistry and biology becomes a huge advantage.

**Q6: How robust are the models for predicting a ligand's position in an unknown protein (generalization)?**

- **Contextual Knowledge:** "Generalization" is an AI model's ability to make accurate predictions on new data it has never seen before. In this context, it means predicting binding for a completely novel protein. An "orthosteric" site is the primary, evolutionarily conserved binding site where the natural substrate binds. An "allosteric" site is a secondary site elsewhere on the protein; when a molecule binds there, it modulates the main site's activity. Allosteric sites are often less conserved and harder to predict.
- **Answer Summary:** **Gabriele Corso** stated this is a major open question. The models generalize well for "well-structured proteins with a lot of evolutionary signal" (implying proteins similar to those in the training data). They struggle significantly with highly dynamic proteins and, importantly, with **allosteric sites**. He concluded that for any specific new target, the best approach is simply to try the model and see.

**Q7: How could data from "failed" clinical trials advance model development?**

- **Contextual Knowledge:** Over 90% of drugs that enter clinical trials fail. They fail due to lack of efficacy, unforeseen toxicity, or poor pharmacokinetics in humans. The detailed data from these failures is a treasure trove of information about what *doesn't* work, which is just as important for training an AI model as data about what *does*. However, this data is almost never made public, creating a huge blind spot for the research community.
- **Answer Summary:** **Najat Khan** gave an emphatic "yes" to the question's premise. She said data from failed trials and even earlier discovery failures would be "incredibly valuable." The fundamental problem is that this corpus of negative data does not exist publicly, and companies have little incentive to share it.

**Q8: What is the new Boltz Gen model and what is its impact?**

- **Contextual Knowledge:** The AI models discussed so far are **predictive**—you give them a molecule, and they predict a property (like binding affinity). **Generative** AI is a step beyond; it *creates* new things. In this context, a generative model like Boltz Gen is designed to create entirely new proteins or molecules from scratch that have a desired property (e.g., "design me a new antibody that binds to this target").
- **Answer Summary:** **Gabriele Corso** explained that Boltz Gen is a generative model for designing new protein binders (peptides, nanobodies, antibodies). **Najat Khan** framed the impact more broadly: open-sourcing such powerful generative tools is critical because the scale of unmet medical need is vast ("80% of drivers of disease don't have therapeutics"). She argues it "unlocks the collective brilliance of innovation," accelerating the entire field toward the shared goal of making new medicines.

---

### Comprehensive Summary

- **Motivation:** The central motivation behind the BOLTS project was to democratize state-of-the-art AI capabilities for drug discovery. Sparked by the limited-access release of AlphaFold 3, the MIT team first developed BOLTS-1 to provide an open-source tool for high-accuracy structure prediction. This laid the groundwork for BOLTS-2, a collaboration with Recursion, which aimed to tackle a more difficult and commercially critical problem: the rapid and accurate prediction of drug-target binding affinity.

- **Central Argument:** The talk's central argument is that open-source, high-performance AI models like BOLTS-2 act as a "force multiplier" that is fundamentally changing the economics and strategy of small molecule drug discovery. By providing near-instant, highly accurate binding affinity predictions, the model allows for a paradigm shift from slow, biased, artisanal lab screening to massive-scale, unbiased, virtual screening. This not only accelerates timelines but also de-risks the pursuit of novel biological targets, a key frontier for future medicines. The panelists argue that while the models themselves are becoming commoditized, true competitive advantage will come from the deep integration of these tools into end-to-end discovery workflows, the generation of high-quality proprietary data in current blind spots, and a relentless focus on solving novel biology.

- **Conclusion:** BOLTS-2 represents a landmark achievement in applying AI to a core challenge in drug discovery. Its open-source release has catalyzed rapid, widespread adoption and created a virtuous cycle of community validation and improvement. The success of BOLTS-2 demonstrates that progress depends on a triad of factors: **algorithmic innovation**, the **curation and generation of high-quality data**, and **collaborative, application-focused partnerships** between academia and industry. The project has not only delivered a powerful tool but has also paved the way for the next frontier: generative AI for therapeutic design, as embodied by the newly released BOLTS Gen.

- **Current Limitations:**
  - **The "Static World" Problem:** While BOLTS-2 incorporates some molecular dynamics data, it still largely operates on static or near-static protein structures. This is a fundamental simplification, as protein flexibility and conformational changes are often critical for drug binding and function.
  - **The Data Limitation:** The model's accuracy is fundamentally constrained by the scope and quality of public training data (e.g., PDB). It may be less reliable for novel protein families or chemical spaces that are not well-represented in these datasets.
  - **Beyond Binding Affinity:** As the panel discussed, high affinity is just one piece of a complex puzzle. The model does not predict other crucial drug-like properties like solubility, permeability, metabolic stability (pharmacokinetics), or off-target toxicity. A predicted "great" binder could still be a terrible drug.
  - **Interpretability:** The models are largely "black boxes." They predict *that* a molecule will bind but don't always provide a clear, chemically intuitive reason *why*, which can make it difficult for medicinal chemists to trust the results and use them to guide the design of new molecules.

- **Alternative Perspectives:**
  - **Physics-Based vs. AI:** The panel positions BOLTS-2 as a much faster alternative to traditional physics-based methods (like Free Energy Perturbation). However, many experts argue that these two approaches are complementary, not just competitive. AI models excel at rapidly screening vast virtual libraries to find promising candidates (a funnel-widening tool), while the more computationally expensive physics-based methods are better for rigorously evaluating a small number of top candidates for lead optimization (a funnel-narrowing tool).
  - **Augmentation over Replacement:** The talk champions an "engineering" approach over an "artisanal" one. An alternative perspective is that these AI tools are not a replacement for the intuition and serendipitous discoveries of experienced medicinal chemists. Instead, they are powerful instruments that augment human expertise, allowing scientists to formulate and test hypotheses at an unprecedented scale and speed.
  - **Open Source vs. Proprietary Models:** Najat Khan argues that competitive advantage lies in proprietary data and workflow integration, not the models themselves. However, some companies are betting heavily on developing superior, proprietary AI models as a key differentiator. The long-term strategic value of a fully open-source versus a closed-source model ecosystem in this space remains an open and actively debated question.

- **Potential Next Steps:**
  1. **From Prediction to Generation:** The immediate next step is the application of generative models like **BOLTS Gen** for the de novo design of protein-based therapeutics (nanobodies, antibodies, etc.).
  2. **Expanding Scope:** Expanding the affinity prediction models to new modalities, including protein-protein interactions, protein-antibody interactions, and covalent ligands.
  3. **Tackling Translational Science:** A major focus for the field is to move beyond binding affinity and develop models that can predict downstream effects like pharmacokinetics (PK), pharmacodynamics (PD), toxicity, and ultimately, human response. This requires new, curated datasets, potentially from "failed" trials and discovery programs.
  4. **Addressing "Hard" Targets:** Improving model performance on scientifically challenging problems, such as predicting the behavior of highly dynamic proteins and targeting allosteric sites.
  5. **Fostering Data Generation:** Advocating for and creating new public and pre-competitive initiatives to generate large-scale, high-quality datasets to train the next generation of models, particularly in areas where data is currently sparse.

## The Business of AI in Drug Discovery

**Speakers:**

- Derek Lowe, PhD, Author of "In the Pipeline"
- Stacie Colad-Thomson, PhD, Business Development Lead, Healthcare and Life Sciences at NVIDIA
- Molly Gibson, PhD, CEO of Expedition Medicines; Origination Partner at Flagship Pioneering
**Coordinator:** Fay Lin, PhD, Senior Editor at GEN

---

### Logical Flow and Sectional Summaries

The panel discussion, moderated by Fay Lin, explores the business and strategic realities of applying AI to drug discovery. It flows from evaluating the current landscape, to identifying the core challenges, and finally to speculating on where future investment should be directed.

#### 1. Hype vs. Reality: Evaluating AI Drug Discovery Companies

- **Contextual Knowledge:** The last decade has seen a massive influx of venture capital into "AI-native" or "tech-bio" startups, each claiming to have a proprietary platform that will revolutionize drug discovery. This has created a crowded and hyped landscape, making it difficult for investors, partners, and talent to distinguish genuine technological advances from ambitious marketing.

- **The Challenge:** How can one evaluate the promise of these countless startups and identify those with a real chance of success?

- **Synthesized Panel Views:**
  - **Derek Lowe (The Realist):** He is immediately turned off by companies still using the "fear of missing out" pitch from a year ago. A realistic pitch is a prerequisite for his attention. Beyond that, he looks for tangible evidence: serious computational resources and, crucially, a team that combines data science experts with seasoned drug discovery veterans.
  - **Molly Gibson (The Pragmatic Builder):** She reframes "hype" as a natural consequence of the industry's fundamental model: making low-probability bets on transformative, high-value outcomes (i.e., a new drug). The key is the "risk-reward calculation." She evaluates companies on their ability to realistically marry the challenge of AI development with the challenge of drug development. Her core criterion is a team with integrated expertise in both building the technology and developing a drug, citing the need to build clinical development expertise at her former company, Generate, to translate the technology.
  - **Stacie Colad-Thomson (The Tech Enabler):** She provides a four-point framework for differentiation:
        1. **Data:** Do they have a differentiated data strategy, such as generating their own unique data?
        2. **Models:** Are they using modern architectures (e.g., transformers)?
        3. **Compute:** Are they making serious investments in compute power?
        4. **Team:** Do they have computational scientists working directly alongside biologists and chemists?

#### 2. The Translation Gap: From Preclinical AI to Clinical Success

- **Contextual Knowledge:** The vast majority of drug development costs and failures (~90%) occur in clinical trials, not in the preclinical phase. An AI platform can discover molecules faster and cheaper, but if those molecules fail in humans at the same rate as traditionally discovered ones, the overall impact on the industry's productivity is minimal. This is known as the "translation gap."

- **The Challenge:** How can AI advancements in the preclinical stage make a meaningful dent in the overall path to an approved drug, given the massive hurdle of clinical development?

- **Synthesized Panel Views:**
  - **Molly Gibson:** She identifies this as a critical issue. The solution is twofold: 1) Solving the **translation problem** by using AI to better predict clinical outcomes (like toxicity) from preclinical data. 2) Improving **clinical decision-making** itself, using AI to optimize trial design, patient selection, dose, biomarkers, and endpoints. In essence, we need to get better at "doing experiments in humans."
  - **Derek Lowe:** He expresses skepticism here, stating his view that AI's current ability to help is almost an *inverse correlation* with the importance of the problem. The hardest, most valuable problems—like target identification and predictive toxicology—remain largely unsolved because our fundamental understanding of human biology is incomplete. However, he remains optimistic in the long term because our biological knowledge and computational power are continuously increasing.
  - **Stacie Colad-Thomson:** She points to early successes where companies like Insilico Medicine and Recursion are getting drugs from target to IND-ready status in 12-18 months. She sees the next step as applying AI to the clinical stage: using LLMs to automate protocol documents, improving patient matching for precision medicine, and even using "digital agents" to improve patient follow-through and data collection during trials, creating a feedback loop to discovery.

#### 3. The Data Gap: From "Small Data" to Foundational Models

- **Contextual Knowledge:** Compared to fields like image recognition or natural language processing which are trained on internet-scale data, biology is a "small data" problem. High-quality, well-annotated biological data is expensive and difficult to generate. The "PDB" (Protein Data Bank) is a rare example of a large, successful, public dataset that enabled the protein structure prediction revolution (AlphaFold, etc.).

- **The Challenge:** How can the field generate the massive, high-quality, fit-for-purpose datasets required to build powerful, generalizable AI models for biology?

- **Synthesized Panel Views:**
  - **Stacie Colad-Thomson:** She identifies two key strategies to close the data gap: 1) **Lab Automation** to create a rapid, closed loop of `Design -> Make -> Test -> Analyze` where an "AI co-scientist" directs robotics to generate new data. 2) **Simulated Data** from computationally intensive, physics-based methods, which is becoming more feasible as compute costs decrease. However, she stresses the ultimate need for better *human-relevant* experimental models (e.g., organoids) to bridge the translation gap.
  - **Derek Lowe:** He tempers the enthusiasm by highlighting the immense complexity, calling the idea of a true "digital cell" one of the greatest potential accomplishments in human history. He points to the constant discovery of new biological mechanisms (e.g., biomolecular condensates, new RNA roles) as evidence of how much we still don't know, suggesting that future scientists will look back on our current knowledge as primitive.
  - **Molly Gibson:** She emphasizes the undeniable success story of the PDB, arguing it might be the most important scientific dataset ever produced. She advocates for a dual approach: 1) Identify and fund the creation of the "next PDB" for other areas like small molecules to enable new foundational models. 2) For specific problems, focus on smaller, high-value, problem-specific models that learn from rapid, iterative experimental loops, which is where integrated lab automation becomes critical.

#### 4. Collaboration vs. Competition: The Open-Source Dilemma

- **Contextual Knowledge:** The tech industry has shown that open-sourcing models and code can accelerate progress for the entire field. However, the biopharma industry is built on protecting intellectual property (molecules, targets, data) as its core commercial asset. This creates a natural tension.

- **The Challenge:** Can the field maintain effective collaboration to move the science forward when strong commercial incentives encourage keeping data and models proprietary?

- **Synthesized Panel Views:**
  - **Derek Lowe:** He notes that the hype itself can hinder collaboration, as each company pitches itself as having a unique "secret sauce." He is also cynical about the historical effectiveness of pre-competitive consortia in pharma, which he feels have under-delivered.
  - **Stacie Colad-Thomson:** She is more optimistic, pointing to new consortia like OpenADMET and Lily TuneLab that are using modern approaches like federated learning to share insights without exposing raw data. She also observes that the influx of talent from the tech industry is bringing a pro-open-source bias, where the competitive advantage shifts from *having* the model to *how quickly you can implement and fine-tune it* with your own proprietary data.
  - **Molly Gibson:** She agrees with the optimistic view, arguing that the field is maturing and starting to understand what is truly a competitive advantage and what is not. As it becomes clear that many foundational models will be commodities, the advantage shifts to the expertise in *using* the model to create a better drug. She also makes a crucial point about the physical reality of biology: it's much harder to share a complex biological assay than it is to share code, which is a practical barrier to collaboration.

#### 5. The Billion-Dollar Question: Where to Invest?

- **The Challenge:** If you had $1 billion to invest in AI-based drug discovery, where would you put it to have the greatest impact?

- **Synthesized Panel Views:**
  - **Molly Gibson (The "Show Me the Value" Take):** She would invest the billion dollars in **getting more AI-generated molecules through clinical trials.** Her reasoning is that the field's biggest challenge is a valuation one; until there are clear, undeniable clinical successes, the true value of AI in early discovery will remain debated and undervalued. Proving the value in humans will lift the entire field.
  - **Stacie Colad-Thomson (The "Close the Loop" Take):** She would invest in technologies that **close the translation gap.** This means funding a combination of "AI co-scientists" (smart reasoning models) that direct automated robotics to generate data from more complex, human-relevant assays. She would want to combine this with Molly's idea of adding in clinical data to create a powerful feedback loop.
  - **Derek Lowe (The "Contrarian Insurance" Take):** Arguing that the field may not be as far along as it thinks, he would invest his billion dollars as "insurance." He would fund **earlier-stage, different, or even orthogonal approaches** that are currently being starved for funds because everyone is chasing the same few popular methods. This would ensure the industry has alternative strategies ready if and when some of the current mainstream approaches fail to deliver on their promise.

---

### Comprehensive Summary

- **Motivation / Central Argument:** The central question of the discussion is whether the immense hype and investment in AI can fundamentally solve the drug discovery industry's core business problem: an astonishingly high failure rate (>85%) and unsustainable costs. The panel's central argument is that while AI is a uniquely powerful technology, it is not a magic bullet. Its success is contingent on overcoming foundational challenges in biology and data. The narrative is shifting from "AI will solve everything" to a more pragmatic focus on where AI can provide tangible value today and what is needed to unlock its transformative potential tomorrow.

- **Conclusion:** The panel concludes that the era of pure hype is ending, replaced by a focus on execution and differentiation. The true value of AI in drug discovery will not come from a single killer algorithm, but from the deep integration of computational tools, automated data generation, and expert human drug developers. The most significant near-term gains are in in-bounded, preclinical problems, but the ultimate prize—improving the clinical probability of success—remains elusive. This will require closing the "translation gap" by developing better human-relevant models and creating a feedback loop from clinical data back to discovery. The future of the field depends on a combination of technological advancement, new models for collaboration, and generating definitive clinical proof points.

- **Current Limitations and Alternative Perspectives:**
  - **Limitations:** The panel identified several key limitations: our profoundly incomplete understanding of human biology; the "small data" nature of biology compared to other fields; the immense difficulty of translating preclinical results to clinical outcomes; and the practical, physical challenges of reproducing and sharing complex biological experiments.
  - **Alternative Perspectives:** The discussion offered several nuanced viewpoints. Molly Gibson reframed **hype** as a necessary component of a high-risk, high-reward industry. Derek Lowe provided a crucial **contrarian** voice, arguing for investing in orthogonal approaches as "insurance" against the failure of mainstream methods, reminding the audience that our current knowledge is likely primitive. This contrasts with the more linear, progress-focused views of the other panelists.

- **Potential Next Steps:** Based on the discussion, the key next steps for the industry are:
    1. **Focus on Clinical Proof:** Push more AI-generated assets into and through clinical trials to definitively demonstrate a higher probability of success and unlock greater value for the entire ecosystem.
    2. **Invest in Human-Relevant Data Generation:** Move beyond simple assays and invest heavily in automated experiments using more complex, human-relevant models like organoids to generate data that is more predictive of clinical outcomes.
    3. **Bridge the Translation Gap with AI:** Apply AI/ML not just to molecule discovery but also to optimizing clinical trial design, patient selection, and endpoint analysis.
    4. **Embrace New Collaboration Models:** Utilize modern technologies like federated learning to enable pre-competitive data and model sharing in a secure, private manner.
    5. **Integrate and Fine-Tune:** Shift the focus of competitive advantage from merely possessing a model to excelling at the rapid implementation and fine-tuning of the best available models (both open-source and proprietary) with high-quality internal data.


## Breakout Session: Building Biology Overnight with Sola (Telesis Bio)

**Speaker:** Daniel Gibson, PhD, Chief Technology Officer at Telesis Bio

---

### Executive Summary

Dr. Daniel Gibson presents the SOLA (Short Oligo Ligation Assembly) platform, an enzymatic DNA synthesis technology developed by Telesis Bio to address the critical bottlenecks in synthetic biology. He contrasts SOLA with traditional phosphoramidite chemical synthesis, highlighting the latter's limitations in speed, cost, fidelity, and environmental impact (hazardous waste). SOLA utilizes a novel, proprietary method of hierarchically assembling short, pre-manufactured DNA building blocks (3-mers and 4-mers) from a universal library. This enzymatic, cell-free process is non-toxic, exceptionally high-fidelity (<1 error per 70,000 bp), and fast, enabling the synthesis of genes up to 4kb in approximately 24 hours. The platform is designed for full automation, integrating with Beckman Coulter robotics (Biomech i7, Echo) to create an on-demand, in-house "biology printer." This gives researchers complete control over their workflow, secures proprietary sequences, and accelerates the design-build-test cycle from weeks or months down to a single day. The technology is commercially validated through a successful collaboration with Pfizer.

---

### Contextual Knowledge

To fully appreciate the talk, understanding these concepts is crucial:

* **Synthetic Biology Design-Build-Test Cycle:** This is the fundamental workflow in bioengineering. Scientists *design* a genetic construct digitally, *build* the physical DNA, and *test* its function in a biological system. The "build" step has historically been the slowest part.
* **Phosphoramidite Chemistry:** For over 40 years, this has been the "gold standard" for chemically synthesizing DNA. It works by adding one nucleotide base at a time to a growing chain. While effective, it has inherent limitations: coupling efficiency is never 100%, leading to errors in the final product, and it requires harsh chemicals, generating significant hazardous waste.
* **Oligonucleotides ("Oligos"):** Short, single-stranded DNA or RNA molecules. They are the fundamental starting materials for building longer genes, acting as primers for PCR, or as probes.
* **Enzymatic DNA Synthesis (EDS):** A newer approach that uses enzymes, rather than harsh chemicals, to synthesize DNA. A common method involves the enzyme Terminal deoxynucleotidyl Transferase (TDT) to add bases one by one. SOLA is a differentiated type of EDS.
* **Gibson Assembly:** A powerful molecular cloning method, also invented by Daniel Gibson, that allows for the joining of multiple DNA fragments in a single, isothermal reaction. It is used in the SOLA workflow to stitch together smaller synthesized fragments into larger constructs (>4kb).
* **PacBio Sequencing (SMRT Sequencing):** A "third-generation" DNA sequencing technology that reads single DNA molecules in real-time. Its long read lengths and high accuracy make it ideal for verifying the fidelity of synthetic DNA constructs without the biases introduced by cloning into bacteria (like *E. coli*).

---

### Delineation and Sectional Summaries

The talk is structured into six logical parts, moving from the general problem to the specific solution and its implementation.

#### 1. The Central Challenge: The DNA Synthesis Bottleneck

* **Challenge Resolved:** Addresses the inefficiency of the "build" phase in the design-build-test cycle for synthetic biology applications (e.g., antibody discovery, genome editing). Researchers face a poor choice: slow, labor-intensive manual synthesis or long, unpredictable, and insecure outsourcing to service providers.
* **Method/Problem Description:** The traditional process is multi-step and slow: oligo synthesis, gene assembly, cloning in *E. coli* for selection and amplification, and plasmid purification. For mRNA, the process is even longer. Outsourcing can take 2-4 weeks for DNA and months for mRNA, creating a highly fragmented and inefficient workflow.
* **Transition:** This inefficiency and lack of control is the core problem that Telesis Bio aims to solve by enabling on-demand, in-house biological printing.

#### 2. Telesis Bio: History and Vision

* **Context:** Establishes the company's deep scientific credibility, tracing its lineage from the J. Craig Venter Institute and Synthetic Genomics. Highlights landmark achievements like the first synthetic genome and minimal cell, which required the development of novel, automated molecular biology tools like Gibson Assembly.
* **Method/Vision:** The core vision was the "Digital to Biological Converter" (DBC), a machine that could autonomously produce DNA, mRNA, and protein from a digital sequence. A 2016 prototype proved the concept but revealed a fatal flaw of chemical synthesis: it generated enormous hazardous waste.
* **Result:** While the fully integrated DBC was impractical due to waste, a key component—the automated DNA assembly module—was robust and successful. This module was commercialized and became the **BioXP instrument**, a cornerstone of Telesis Bio's business.

#### 3. Introducing the SOLA Platform

* **Challenge Resolved:** Moves beyond the limitations of the BioXP (which still relies on externally sourced oligos) to a fully in-house, on-demand synthesis solution.
* **Method/Platform Description:** SOLA is introduced as an **enzymatic, non-toxic, and scalable DNA/RNA synthesis platform**. It consists of three parts:
    1. **Reagents:** Make-to-stock, universal reagent kits.
    2. **Software:** For sequence validation and automated workflow generation.
    3. **Automation:** Implemented on standard lab robotics (in collaboration with Beckman).
* **Result/Value Proposition:** SOLA bridges the gap between discovery and screening by:
  * **Accelerating Timelines:** From weeks/months to days.
  * **Boosting Efficiency:** Redeploying scientists from manual labor to strategic work.
  * **Ensuring Workflow Control:** Keeping proprietary sequences and processes secure within the user's facility.

#### 4. SOLA: Technical Deep Dive

* **Challenge Resolved:** Explains *how* SOLA overcomes the fidelity, cost, and waste problems of chemical synthesis.
* **Method - SOLA (Short Oligo Ligation Assembly):** This is the core technical reveal.
    1. **Universal Building Blocks:** SOLA does not add single bases. It uses a pre-manufactured, universal library of **1,280 short oligos** (3-mers and 4-mers).
    2. **Hierarchical Assembly:** The system enzymatically ligates these blocks in five stages to build a 100-mer fragment (e.g., 3-mer + 4-mer → 7-mer → 10-mer → ... → 100-mer).
    3. **Inherent Error Correction:** The hierarchical process is self-correcting. Only perfectly ligated fragments can participate in the next stage of assembly; imperfect or mutated pieces are naturally "weeded out."
    4. **Final Assembly:** These high-fidelity 100-mer fragments are then assembled into full-length genes using established methods like Gibson Assembly.
* **Result:** This method leads to significant advantages:
  * **Fidelity:** Coupling efficiencies approach 100%, far exceeding the ~99.5% of chemical synthesis, resulting in virtually error-free DNA.
  * **Cost:** The universal building blocks can be used millions of times, amortizing the cost exponentially compared to single-use custom oligos.
  * **Waste:** The entire process is enzymatic and aqueous, generating only non-toxic waste.

#### 5. SOLA: Performance Data and Specifications

* **Challenge Resolved:** Provides quantitative proof of the platform's capabilities.
* **Results/Specifications:**
  * **Length:** Routinely builds fragments up to 4kb. Larger constructs (e.g., 9.6kb example) are made by stitching 4kb pieces together with Gibson Assembly.
  * **Purity:** >90% full-length product (data shows ~95% average).
  * **Fidelity:** Specification is <1 error per 70,000 base pairs. PacBio sequencing data shows an achieved fidelity of **1 error per 180,000 base pairs**, significantly better than spec. Sanger sequencing of cloned genes confirms the vast majority of clones are perfect.
  * **Complexity (GC Content):** Specification is 30-60% GC. Data shows successful builds up to 68% GC, demonstrating flexibility.
  * **Buildability:** >95% success rate for sequences in the database, with a predicted success rate of ~99%.
* **Note on Transcription:** The text mentions "DNA scallop," which is a likely transcription error for "DNA scale-up."

#### 6. Automation and Commercialization

* **Challenge Resolved:** Demonstrates how SOLA is implemented in a real-world lab setting to deliver on its high-throughput promise.
* **Method:** The semi-automated workflow is being collapsed onto a fully automated platform using **Beckman Coulter's Biomech i7 workstation** and an **Echo acoustic liquid handler**. This combination allows for precise, low-volume liquid handling and walk-away operation.
* **Result/Throughput Tiers:**
  * **Low:** Standalone Biomech i7 (~20kb/week).
  * **Medium:** Biomech i7 + Echo (tens of kb/day).
  * **High:** Beckman Access workstation (hundreds of kb/day).
* **Commercial Validation:** The talk concludes by noting a multi-year collaboration with **Pfizer**, where the SOLA technology is now being used autonomously by Pfizer scientists, validating its robustness and utility in a pharmaceutical R&D environment.

---

### Comprehensive Final Summary

* **Motivation:** The primary motivation is to solve a critical pain point in modern biology: the "build" phase of the design-build-test cycle is a major bottleneck. Existing methods for acquiring synthetic DNA are slow, expensive, error-prone, generate hazardous waste, and force companies to send proprietary genetic sequences to third-party vendors.

* **Central Argument:** The central argument is that Telesis Bio's SOLA platform is a disruptive technology that fundamentally solves these problems. By shifting from single-base chemical synthesis to a hierarchical, enzymatic assembly of universal building blocks, SOLA enables a fast, high-fidelity, clean, and cost-effective method for on-demand DNA synthesis that can be fully automated and brought in-house.

* **Conclusion:** The SOLA platform is presented as a mature and validated solution that transforms DNA synthesis from a multi-week outsourced service into an overnight, in-house, automated process. This allows research organizations to accelerate discovery, maintain control and security over their intellectual property, and ultimately enhance productivity in therapeutic development.

* **Current Limitations:**
  * The standard build length is capped at ~4kb, requiring an additional Gibson Assembly step for larger genes or pathways.
  * The specified GC content range is 30-60%, and while the boundaries can be pushed, extremely high or low GC content and complex repeats may still pose challenges or require workflow modifications.
  * The fully automated, high-throughput versions rely on a specific ecosystem of expensive capital equipment (Beckman and Echo liquid handlers).

* **Alternative Perspectives:** The talk positions SOLA against two main alternatives:
    1. **Phosphoramidite Chemistry:** The incumbent "gold standard," which SOLA surpasses in fidelity, speed (for the end-user), and environmental safety.
    2. **TDT-based Enzymatic Synthesis:** Another emerging technology. Gibson argues SOLA is superior, particularly in fidelity, due to its unique block-based assembly and inherent error-correction mechanism.

* **Potential Next Steps:**
  * **Full Integration with AI:** The talk hints at integrating AI models to enhance predictive power. The next logical step is to create a fully closed loop where AI designs novel constructs, SOLA builds them overnight, and high-throughput screening tests them, with the results feeding back into the AI for the next design iteration.
  * **Expanding Build Complexity:** Further R&D to reliably synthesize DNA with very high/low GC content, long homopolymer runs, and other complex repetitive structures that are challenging for all synthesis methods.
  * **Increasing Accessibility:** Developing lower-cost or smaller-footprint automation solutions to make the technology accessible to a wider range of academic and smaller industrial labs.

## Multimodal AI for Healthcare

> [scGPT paper](https://www.nature.com/articles/s41592-024-02201-0)
> [scGPT github](https://github.com/bowang-lab/scGPT)
> [The Multi-modality Cell Segmentation Challenge: Towards Universal Solutions](https://arxiv.org/abs/2308.05864): NeurIPS challenge 2023 (microscopy images)
> [MedSAM github](https://github.com/bowang-lab/MedSAM): [Segment Anything](C_Albicans%20Thesis%20Project/6.%20References/Segment%20Anything.md) applied for medical images (x rays, CT scans, and pathology images)
> [Towards multimodal foundation models in molecular cell biology](https://www.nature.com/articles/s41586-025-08710-y)
> [How to Build the Virtual Cell with Artificial Intelligence: Priorities and Opportunities](https://arxiv.org/abs/2409.11654)
> [BioReason: Incentivizing Multimodal Biological Reasoning within a DNA-LLM Model](https://arxiv.org/abs/2505.23579)

**Speaker:** Bo Wang, PhD, SVP and Head of Biomedical AI at Xaira Therapeutics

---

### Executive Summary

Dr. Bo Wang presents a compelling narrative on the successful application of the "foundation model" paradigm to complex biological data. He details the journey of creating **scGPT**, one of the first foundation models for single-cell genomics, and **MedSAM**, a highly successful foundation model for medical image segmentation. The central argument is that large-scale, pre-trained transformer models can serve as a unifying framework, replacing the fragmented ecosystem of task-specific specialist models.

Dr. Wang explains how scGPT, pre-trained on 33 million cells, can be fine-tuned to outperform state-of-the-art methods in tasks like batch correction and cell-type annotation. He then pivots to the challenge of imaging, describing how MedSAM was created by transfer learning from Meta's general-purpose SAM model. MedSAM achieves remarkable zero-shot performance across diverse medical imaging modalities. The talk concludes with a forward-looking vision of building a multimodal "AI Virtual Cell" and enabling biological reasoning by integrating genomic and language models, as demonstrated by the **BioReason** project. The Q&A session further explores the technical nuances and broad applicability of these models in biomedical research and drug discovery.

---

### Contextual Knowledge

* **Foundation Model:** A term coined by Stanford researchers for large-scale AI models (typically Transformers) pre-trained on vast amounts of data. The key idea is that a single pre-trained model can be adapted (usually via fine-tuning) to a wide range of downstream tasks, acting as a "foundation" for many applications. ChatGPT is the most famous example.
* **Single-Cell RNA-Seq (scRNA-seq):** A revolutionary technology that measures the gene expression (which genes are "on" or "off") of thousands of individual cells at once. This provides a high-resolution snapshot of cellular states, heterogeneity, and dynamics.
* **Transformer Architecture:** The deep learning architecture that underpins most modern foundation models. Its key innovation is the "attention mechanism," which allows the model to weigh the importance of different parts of the input data, making it highly effective for modeling complex dependencies in sequential data like text or, in this case, genes.
* **Batch Effect:** Technical, non-biological variation between scRNA-seq datasets that arises from being processed in different batches (e.g., on different days, by different people, or with different reagent lots). Removing batch effects is a critical step for integrating data from multiple experiments.
* **Zero-Shot Learning:** The ability of a model to perform a task it was not explicitly trained to do. For example, MedSAM segmenting a type of tumor it has never seen before. This is a hallmark of a powerful, generalizable foundation model.
* **Fine-Tuning:** The process of taking a pre-trained foundation model and continuing to train it on a smaller, task-specific dataset to adapt it for a particular application. This is much more computationally efficient than training a model from scratch.

---

### Delineation and Sectional Summaries of the Talk

The talk is structured as a journey, starting with the abstract concept of foundation models and demonstrating their concrete, successful application in two distinct biological domains.

#### 1. Introduction: The Foundation Model Paradigm

* **Challenge Resolved:** Establishes a clear framework for the subsequent projects. Instead of seeing AI in biology as a collection of disparate tools, it frames the goal as building unified, general-purpose models.
* **Method/Concept:** Dr. Wang introduces the "ABCD" of foundation models:
  * **A**lgorithms: Deep learning, primarily the Transformer architecture.
  * **B**ig Business: One model enabling multiple applications via transfer learning.
  * **C**omputing: Requires specialized hardware like GPUs/TPUs.
  * **D**eep Data: Requires massive datasets for pre-training.
* **Transition:** This framework sets the stage for the central question: Can this paradigm, proven in language and vision, be applied to single-cell biology?

#### 2. scGPT: A Foundation Model for Single-Cell Genomics

* **Challenge Resolved:** Addresses the "one task, one model" problem in single-cell analysis, where biologists must choose from a zoo of specialist tools for different analytical tasks (e.g., batch correction, cell typing).
* **Method (with added technical detail):**
    1. **Data (D):** Curated a massive dataset of 33 million human cells from the Human Cell Atlas.
    2. **Algorithm (A):** Developed **scGPT**, a GPT-style (decoder-only) Transformer model. A key innovation was adapting it for non-ordered gene data through:
        * **Novel Tokenization:** The input for each cell is a sequence of tokens. This includes: (1) **Gene ID tokens**, representing the specific genes expressed. (2) **Expression value tokens**, where continuous expression values are discretized into 55 bins, turning a regression problem into a classification problem suitable for a GPT architecture. (3) **Condition tokens**, which embed metadata like sequencing technology, tissue of origin, disease state, or patient ID, allowing the model to learn and control for these variables.
        * **Cell-Specific Causal Masking:** Unlike words in a sentence, genes have no natural order. To use a GPT-like "next-token prediction" objective, scGPT creates a cell-specific gene order. For each cell, it ranks genes based on their attention scores relative to a special `[CLS]` (cell) token. The model is then trained to predict the expression of lower-ranked (less contextually important) genes using the higher-ranked (more important) ones. This dynamically creates a biologically-aware hierarchy for each cell.
    3. **Computing (C):** Pre-training took 2 weeks on 20 NVIDIA A100 GPUs. Model has 15 million parameters.
    4. **Fine-Tuning:** The pre-trained model is adapted using task-specific loss functions. For multi-batch integration, this involved:
        * **Contrastive Loss:** Pulls embeddings of biologically similar cells closer together and pushes dissimilar ones apart, preserving biological identity.
        * **Adversarial Loss:** A secondary "discriminator" network is trained to predict a cell's batch origin from its embedding. The main scGPT model is simultaneously trained to generate embeddings that *fool* this discriminator, thereby removing batch-specific information.
* **Results:**
  * When fine-tuned, scGPT significantly outperformed established, state-of-the-art specialist methods like Seurat v3 and SVI for multi-batch integration and SCBERT for cell-type annotation.
  * This demonstrates the "Big Business" (B) principle: one foundational model can excel at multiple applications.
* **Limitations & Transition:** Dr. Wang candidly calls this a "GPT-2 moment" for single-cell biology. The model is powerful but has limitations: it's restricted to RNA-seq, is correlational (not causal), and requires fine-tuning for complex tasks (limited zero-shot ability). This leads to the next question: can this be extended to other data types, like images?

#### 3. MedSAM: A Foundation Model for Medical Imaging

* **Challenge Resolved:** Addresses the data scarcity problem in *biological* imaging and the "one model per modality" issue in *medical* imaging. While a foundation model for biological microscopy images remains difficult due to a lack of large, diverse public datasets (a conclusion from a NeurIPS competition Dr. Wang's lab organized), the medical imaging domain is more data-rich.
* **Method (with added technical detail):**
    1. **Starting Point (Transfer Learning):** Instead of training from scratch, they leveraged Meta's **Segment Anything Model (SAM)**. SAM's architecture consists of: (a) a powerful Vision Transformer (ViT) image encoder that creates a rich embedding of the image, (b) a prompt encoder for points, boxes, or text, and (c) a fast mask decoder that generates a segmentation mask from the image embedding and prompt.
    2. **Continued Pre-training:** They took the pre-trained SAM image encoder and fine-tuned it on a curated dataset of **1 million medical image-mask pairs**. This process, also known as domain adaptation, specializes the encoder's features (which already understand general concepts like edges and textures) to recognize specific patterns in medical images, such as tissue boundaries or tumor morphologies.
    3. **The Result:** This process created **MedSAM**. Its power comes from the generality of the promptable segmentation framework combined with the specialized knowledge of the fine-tuned encoder.
* **Results:**
  * MedSAM demonstrates outstanding **zero-shot** performance, accurately segmenting organs, tumors, and cells across a wide variety of medical imaging types without any task-specific fine-tuning.
  * It dramatically outperforms specialist models in head-to-head comparisons.
  * The model has been cited over 2,500 times in under a year, showing massive and rapid adoption by the medical community. This highlights the immense value of a single, general-purpose tool.

#### 4. Future Vision: The AI Virtual Cell and Multimodal Reasoning

* **Challenge Resolved:** Moves beyond single-modality models to the ultimate goal of creating a comprehensive, reasoning model of a cell.
* **Method/Vision:**
    1. **The AI Virtual Cell:** The vision is to build next-generation AI models that integrate multiple data modalities (genomics, proteomics, imaging) to create a holistic, predictive model of cellular biology.
    2. **Multimodal Reasoning:** The key is to enable these models to *reason*. Dr. Wang introduces **BioReason**, a recent project where they combined a DNA foundation model (Evo) with a large language model (LLM). By using the LLM to generate "reasoning traces," they successfully aligned the DNA tokens with language tokens, boosting the model's ability to interpret genomic sequences.
* **Conclusion:** This points to a future where foundation models for different biological data types are not just used in isolation but are integrated and guided by the reasoning capabilities of LLMs to unlock a deeper, more causal understanding of biology.

---

### Summary of Q&A Session with Contextual Background

The Q&A provides deeper technical insights and practical advice on using these models.

**1. Q: What is the effect of different sequencing technologies (e.g., 10x vs. Smart-seq) on the model?**

* **Contextual Background:** This question addresses data heterogeneity. 10x Genomics captures the 3'-end of transcripts and uses Unique Molecular Identifiers (UMIs) for more accurate quantification, while Smart-seq2 provides full-length transcript coverage but can suffer from amplification bias. These technical differences create distinct data distributions that could confuse a model.
* **Answer Summary:** scGPT was pre-trained on diverse technologies. This is handled by using "condition tokens" to inform the model of the data source. This diversity is beneficial as it exposes the model to varied data distributions, improving its robustness and generalization.

**2. Q: Can scGPT be used for bulk RNA-seq data?**

* **Contextual Background:** This probes the model's flexibility. Bulk RNA-seq measures the average gene expression across a population of cells, whereas scGPT is trained on individual cell profiles. Applying a single-cell model to bulk data is not straightforward, as the input data represents a mixed signal.
* **Answer Summary:** Yes. While not in the original paper, other researchers have successfully used the pre-trained scGPT gene embeddings for bulk RNA-seq analysis. Dr. Wang's team is now working on formally extending the model to jointly handle both data types.

**3. Q: Can you give examples of "reasoning" in BioReason?**

* **Contextual Background:** This asks for clarification on the ambitious claim of enabling AI to "reason" about biology. In AI, reasoning means the model isn't just pattern matching but is manipulating knowledge to draw inferences. A "reasoning trace" is a step-by-step explanation of this process.
* **Answer Summary:** BioReason combines a DNA foundation model (Evo) with an LLM. The LLM generates explanatory text about a DNA sequence (e.g., "This sequence is a promoter because it contains a TATA-box at this position, which recruits RNA polymerase"). Reinforcement learning is then used to align the raw DNA sequence embeddings with the language embeddings of this explanation, teaching the model to connect sequence patterns to their functional meaning.

**4. Q: Are causal models used in BioReason?**

* **Contextual Background:** This is a critical question about the depth of the model's understanding. Most deep learning models are correlational (they learn that A and B often appear together). A causal model would understand if A *causes* B. In genomics, this is the holy grail for understanding gene regulation and predicting the true effect of a drug.
* **Answer Summary:** Not yet. Currently, the reasoning chains are generated by human experts and LLMs, which are themselves largely correlational. Dr. Wang agrees that incorporating formal causal discovery methods or causal knowledge graphs is a key and promising future direction.

**5. Q: How can traditional drug discovery companies leverage these frameworks?**

* **Contextual Background:** This question seeks to bridge the gap between academic AI research and industrial application. Drug discovery involves a long pipeline (target ID, lead optimization, preclinical testing), and it's important to know where these new tools can provide tangible value.
* **Answer Summary:** Dr. Wang sees huge potential. Examples include using AlphaFold for target structure prediction, diffusion models for antibody design, and agentic systems to integrate these tools. Foundation models like scGPT can be used for target identification, understanding a drug's mechanism of action (MoA), and in-silico toxicity prediction.

**6. Q: How transferable are scGPT embeddings to other tasks?**

* **Contextual Background:** This question tests the core premise of a foundation model. An "embedding" is a dense numerical vector representing an object (like a cell). If the model has learned a truly meaningful representation, its embeddings should be useful for many downstream tasks, even ones it wasn't explicitly trained on. This is known as transfer learning.
* **Answer Summary:** Highly transferable. This is the model's purpose. The paper demonstrates applications beyond cell-typing, including multi-omic integration, gene regulatory network inference, and perturbation response prediction. The goal is one generalist model for many tasks.

**7. Q: Can scGPT be used for non-human species?**

* **Contextual Background:** This addresses the model's scope. Biological mechanisms are often conserved across species, but gene names and functions can diverge. A multi-species model would need to understand orthologs (genes in different species that evolved from a common ancestral gene) and handle the complexities of evolutionary divergence.
* **Answer Summary:** The original model is human-only; a mouse version was also released. A true multi-species model is challenging because of the difficulty in defining and aligning orthologous genes. It's an active area of research.

**8. Q: Have you combined scRNA-seq data with RNA structure models?**

* **Contextual Background:** This is a forward-thinking question about multimodality. An RNA molecule's function is determined not just by its sequence but by its 3D structure. Integrating structural information could provide a much richer signal for the model, but this requires accurate structure prediction and a method to combine it with expression data.
* **Answer Summary:** An "amazing question." They have considered it, but it's very challenging. The main hurdles are (1) the lack of highly accurate, generalizable RNA structure prediction models and (2) the technical difficulty of integrating structural priors into the scGPT training process.

**9. Q: How well does scGPT work on rare diseases?**

* **Contextual Background:** This probes the model's robustness and clinical utility. Foundation models are trained on large, common datasets. Their ability to perform well on "long-tail" phenomena, like rare cell types or diseases that were underrepresented in the training data, is a critical test.
* **Answer Summary:** It can work well, but **fine-tuning is highly recommended** for any domain or disease the model has not seen during pre-training. The scGPT GitHub provides detailed tutorials for this.

**10. Q: Is the Transformer the right architecture for a "virtual cell"?**

* **Contextual Background:** This question touches on the cutting-edge of AI research. While Transformers are dominant, they have quadratic complexity with sequence length, making them computationally expensive for very long sequences (like a full genome). Newer architectures like State Space Models (Mamba) and Hyena have been proposed as more efficient alternatives.
* **Answer Summary:** Dr. Wang believes the Transformer is the most promising and direct path for now. However, he is open to other architectures, stressing that the combination of a good model architecture and a massive dataset is what truly matters.

**11. Q: How practical is the AI-driven "virtual cell" today?**

* **Contextual Background:** This is a reality-check question. It distinguishes between success on academic benchmarks (e.g., achieving high accuracy on a public dataset) and delivering practical value in a commercial setting (e.g., identifying a viable drug target that leads to a real therapeutic).
* **Answer Summary:** The field is new, and robust, practical benchmarks are still lacking. The true test will be adoption in drug discovery for high-value tasks like target ID, MoA detection, and toxicity prediction.

**12. Q: Does scGPT translate to proteomics data?**

* **Contextual Background:** This question explores cross-modality transfer. According to the central dogma of biology, RNA is translated into protein. However, RNA levels and protein levels are often poorly correlated. A model trained only on RNA data that can still generate useful embeddings for protein data would be a powerful result, suggesting it has learned fundamental biological relationships.
* **Answer Summary:** Surprisingly well. The gene embeddings from scGPT have proven useful for downstream proteomics tasks. However, performance would be significantly boosted by training on a true multi-omic dataset that jointly profiles both RNA and proteins.

---

### Comprehensive Final Summary

* **Motivation:** The field of computational biology is fragmented, with a vast number of specialized, often incompatible, tools for narrow tasks. This complicates analysis, hinders generalization, and slows down research. The motivation was to apply the unifying "foundation model" paradigm from mainstream AI to create single, general-purpose models for complex biological data.

* **Central Argument:** Dr. Wang argues that large-scale, self-supervised pre-training on massive biological datasets is a transformative approach for biology. A single foundation model, like scGPT for single-cell genomics or MedSAM for medical imaging, can replace an entire ecosystem of specialist tools, providing superior performance, simplifying workflows, and enabling novel capabilities (like zero-shot segmentation).

* **Conclusion:** The foundation model paradigm is not just a theoretical concept but a practical success in biomedicine. scGPT established a new direction for single-cell analysis, proving a generalist model can outperform specialists. MedSAM took this a step further, demonstrating the power of transfer learning to achieve incredible zero-shot performance, leading to its rapid global adoption. The future is to build upon these successes to create multimodal, reasoning "AI Virtual Cells."

* **Current Limitations:**
  - **High Pre-training Cost:** Creating these models from scratch requires massive compute resources, limiting their development to well-funded academic labs or industry.
  - **Data Scarcity:** While some domains are data-rich (human scRNA-seq, medical images), others are not (biological microscopy, non-human genomics), which is the primary barrier to building foundation models for them.
  - **Need for Fine-Tuning (scGPT):** scGPT's "GPT-2" level of development means it still requires task-specific fine-tuning for optimal performance, lacking the powerful zero-shot capabilities of more mature models.
  - **Correlational Nature:** These models learn complex statistical associations from data but do not inherently understand causality.

* **Alternative Perspectives:** The primary alternative is the status quo: a rich ecosystem of specialized models (e.g., Seurat, SVI). These tools are often highly optimized for their specific task but lack the generality and unifying potential of a foundation model. The talk argues for a paradigm shift away from this fragmented approach.

* **Potential Next Steps:**
  - **True Multimodality:** Building models that are pre-trained from the start on integrated, multi-omic data (e.g., RNA + ATAC + protein + spatial data) to learn a more holistic cellular representation.
  - **Causal Reasoning:** Moving beyond correlation by incorporating causal structures, perturbation data, and biological knowledge graphs directly into the model architecture and training process.
  - **Improving Zero-Shot Performance:** Pushing single-cell models like scGPT towards a "GPT-4 moment" where they can perform complex tasks accurately with little to no fine-tuning.
  - **Agentic AI Systems:** Creating AI agents that can use these foundation models as tools to autonomously design experiments, analyze data, and form new hypotheses, fully closing the design-build-test loop.

### Information on Xaira Therapeutics

Here’s a concise summary of Xaira Therapeutics:

* **Headquarters / Location:** Based in the San Francisco Bay Area (South San Francisco, CA) with additional offices in Seattle and London. 
* **Scope of business:** It is an integrated biotech company that uses artificial intelligence to transform drug discovery and development—from uncovering biological understanding all the way through to therapeutic product development.
* **Key technological strengths:**
  * Advanced AI research and foundational computational methods (e.g., generative models for protein design) drawing on work from the Institute for Protein Design.
  * Large-scale data generation and integration platforms (multi-omic, functional genomics, proteomics) to fuel model training and biology discovery.  **X-Atlas/Orion** is a perturbation-seq (Perturb-seq) dataset covering ~8 million cells, intended to fuel the “virtual cell” modeling community.
  * An end-to-end drug pipeline that bridges model design → molecule engineering → biological/therapeutic testing, enabling iterative feedback between computational models and experimental data.

## Building the Virtual Cell

**Panelists:**
* **Theofanis (Theo) Karaletsos, PhD:** Senior Director of Artificial Intelligence, Chan Zuckerberg Initiative (CZI)
* **Hani Goodarzi, PhD:** Core Investigator, Arc Institute; Associate Professor, UCSF
* **Emma Lundberg, PhD:** Associate Professor, Stanford; Professor, KTH Royal Institute of Technology
* **Ron Alfa, MD, PhD:** Co-founder and CEO, NOETIK

---

### Executive Summary

This panel discussion convenes four leaders from academia and industry to dissect the ambitious goal of building a "virtual cell." The consensus is that a virtual cell is not a single, monolithic, reductionist simulation of biochemistry, but rather a suite of predictive, data-driven AI models that operate across multiple biological scales. The panelists advocate for a utilitarian approach, starting with models that are immediately useful to biologists—such as predicting cellular responses to genetic perturbations—and progressively building towards a more comprehensive, multi-scale, and multimodal understanding of cellular and organismal biology. Key themes include the critical need for strategic, fit-for-purpose data generation (especially spatial and proteomic data), the shift from using wet labs for hypothesis search to hypothesis validation, and the necessity of community-wide collaboration through competitions and shared benchmarks to tackle a problem far less defined than previous AI triumphs like protein folding.

---

### Contextual Knowledge

* **Virtual Cell:** A conceptual framework for a computational model that can simulate the behavior of a biological cell. Its goal is to predict how a cell will respond to various stimuli, such as genetic perturbations or drugs, and to understand the underlying mechanisms of cellular function in health and disease.
* **Multimodal & Multi-scale Data:** Biological data comes in many forms (**modalities**) like transcriptomics (RNA), proteomics (protein), genomics (DNA), and imaging. These can be measured at different levels of organization (**scales**), from single molecules to cells, tissues, and whole organisms. Integrating these is a grand challenge.
* **Perturbation:** The act of intentionally disturbing a biological system to observe its response. This is a cornerstone of experimental biology. **Genetic perturbations** (e.g., gene knockdowns using CRISPR) are a common way to infer gene function.
* **Spatial Omics:** A revolutionary class of techniques that measure molecular data (like RNA or protein expression) while preserving the spatial context of the cells within a tissue. This allows researchers to study not just what cells are present, but how they are organized and interact in their native environment.
* **Causal Biology:** The study of cause-and-effect relationships in biological systems (e.g., does protein A *cause* disease B?). This is distinct from correlational analysis and is essential for identifying effective therapeutic targets.
* **CASP (Critical Assessment of protein Structure Prediction):** A community-wide, biennial competition that was instrumental in driving progress in protein structure prediction, culminating in the success of models like AlphaFold. It is often cited as a model for how to organize a scientific community to solve a grand challenge.

---

### Delineation of Panel Discussion by Topic

The discussion was organized around four central themes, with each panelist providing a unique perspective.

#### Topic 1: Defining the "Virtual Cell"

The panel collectively rejected a narrow, reductionist definition in favor of a broader, more functional, and multi-faceted vision.

* **Theo Karaletsos (CZI):** Proposed a broad vision of a **multi-scale model** that represents biology from the molecular level up to the organism. He emphasized that "virtual cell" is not a single endpoint but a collection of useful models at different levels of abstraction. He sees the popular definition—a model that predicts transcriptomic response to genetic perturbations—as a valid and tremendously useful *initial target state*, but not the final goal.

* **Hani Goodarzi (Arc Institute):** Added a **utilitarian view**. A virtual cell model has succeeded when a cell biologist can use it *in lieu of* an experimental model for initial hypothesis testing. He argued that focusing on perturbation and transcriptomics is a pragmatic starting point because it directly mirrors the primary lens through which systems biology has operated for the past 20 years.

* **Ron Alfa (NOETIK):** Provided a contrast, stating a virtual cell is **not a "bag of biochemistry" simulation**. At NOETIK, the virtual cell is used as a **probe** to build understanding from the single-cell level up to the patient. The immediate goal is to use simulations to understand patient biology in the context of health and disease, making it directly applicable to therapeutic hypotheses today.

* **Emma Lundberg (Stanford/KTH):** Agreed with Ron, highlighting the promise of these models to understand **emergent properties across scales**. She stressed that biology operates across vast scales—from molecular changes to organism-level phenotypes—and the true power of virtual cell models lies in their potential to interpret these complex, multi-scale connections, which are incredibly difficult to measure experimentally.

#### Topic 2: Therapeutic Applications

The panelists described a paradigm shift where in-silico models handle initial discovery, allowing expensive lab work to be focused on validation.

* **Theo Karaletsos:** The primary application is to empower **causal biology**—identifying causal targets and patient cohorts for drug discovery. He envisions a future where the laborious "search for hypotheses" is moved from the wet lab to in-silico experimentation. As he puts it, the wet lab shouldn't be a means of search, but a **means of validation**.

* **Hani Goodarzi:** Framed all disease modeling (including cell lines and mouse models) as an abstraction of the true, unattainable system within a patient. He argued that in-silico models have a key advantage: they can **go beyond the ceiling of experimental models**, which are imperfect recapitulations (e.g., a mouse model of a human disease).

* **Ron Alfa:** Described two concrete applications at NOETIK, which works with static, multimodal data from human tumor pathology specimens:
    1. **Understanding Patient Biology:** They simulate the placement of virtual cells in different tissue contexts to build a rich representation space of patient biology, which is then used to identify therapeutic targets or train classifiers for predicting patient response to therapy.
    2. **Simulating Perturbations:** They use the virtual cell to simulate the effect of perturbations on this static patient data, allowing them to perform *in-silico experiments* on data that cannot be physically manipulated.

#### Topic 3: The Data Challenge

This was a central theme, with all panelists agreeing that data strategy is paramount and that we are in a new era where AI needs are driving data generation.

* **Emma Lundberg:** Emphasized that we don't yet know which data modalities will be most valuable. While transcriptomics is currently scalable, she champions the importance of **protein-level measurements** (proteomics), as proteins are the direct executors of cellular function and structure. She highlighted the challenge of modeling the sub-cellular scale (molecule-to-cell) and the need for community synergy to generate well-paired multimodal datasets.

* **Ron Alfa:** Stated that NOETIK started from the premise that the necessary data didn't exist and had to be generated. Their strategy is to create **fit-for-purpose, multimodal, and spatial data** from the outset, using images as a core data type across modalities (H&E, protein, spatial transcriptomics). This ensures that tissue context and cellular interactions are embedded in the model from day one. He noted their strategy is constantly evolving as they learn which data provides the most predictive power.

* **Hani Goodarzi:** Made two critical points:
    1. **A New Era:** For the first time, AI/ML experts are telling biologists what data they need, a major shift in the dynamic.
    2. **The Scale of Data:** Drawing a parallel to NLP, where models showed emergent properties after being trained on ~1 trillion tokens, he suggested biology may need even *more* data because it is less information-dense (more redundant) than human language. This means we must invest in improving data generation technologies themselves.

* **Theo Karaletsos:** From an ML perspective, data strategy must be tied to the goal. He differentiated between data for **general pre-training** (modeling "life as it exists" from large public atlases) and data for **specific applications** (honing in on a biological space with targeted perturbations). He argued that designing the data collection strategy and the potential need for a "curriculum" to teach the models is the true frontier, perhaps even more important than the model architecture itself.

#### Topic 4: Fostering Collaboration and Defining Success

The panel discussed how to organize the community to tackle such a complex and ill-defined problem.

* **Hani Goodarzi:** Pointed to **CASP** as the success story for protein folding. To replicate this, the Arc Institute has launched the **Virtual Cell Challenge**, an annual competition where teams apply their models to a high-quality, unseen genetic perturbation dataset. The goal is to create an equal footing for comparison and, just as importantly, to build a vibrant community through platforms like Discord where scientists can interact and collaborate.

* **Emma Lundberg:** Agreed that competitions are great anchor points, but highlighted a key difference: the virtual cell problem is **far less well-defined than protein folding**. A virtual cell is expected to have many capabilities across different scales (predicting transcriptomes, cell-cell interactions, etc.). The next major challenge for the community is to converge on a set of **core capabilities and define how to measure success** broadly across all of them, rather than focusing on single-modality benchmarks.

---

### Comprehensive Final Summary

* **Motivation:** The fundamental motivation is to create predictive, computational models that can grapple with the immense complexity of biology across different scales—from molecules to cells to tissues and organisms. This is a task that is intractable with purely experimental methods and is seen as the next grand challenge for AI in biology.

* **Central Argument:** The panel collectively argues that building a "virtual cell" is a pragmatic, step-wise process, not a single moonshot. The path forward is not through reductionist, first-principles simulation, but through data-driven, machine learning models that learn from massive, multimodal, and strategically generated biological data. The immediate goal is to create models that are demonstrably useful to biologists, thereby creating a virtuous cycle where in-silico experimentation accelerates discovery and guides more targeted wet-lab validation.

* **Conclusion:** The concept of the virtual cell is maturing from a vague idea into a tangible, albeit complex, research program. The field is converging on a strategy that prioritizes: (1) A utilitarian focus on useful, predictive models (like perturbation response). (2) A massive, community-wide effort in strategic, fit-for-purpose data generation, with a focus on spatial and multimodal data. (3) The creation of a collaborative ecosystem, anchored by competitions and shared benchmarks, to drive progress in a coordinated way.

* **Current Limitations:**
  - **Ill-Defined Problem:** Unlike protein folding, the "virtual cell" lacks a single, clear objective function, making it difficult to measure success.
  - **Data Bottleneck:** The scale of data required is immense, and the most informative data modalities and combinations are still under investigation.
  - **Correlational Models:** Current AI models are primarily correlational and do not inherently understand causality, which is a key goal of this endeavor.

* **Alternative Perspectives:** The main alternative discussed and rejected by the panel is the idea of a "bag of biochemistry"—a first-principles, physics-based simulation of all molecular interactions in a cell. The panelists favor a more phenomenological, data-driven machine learning approach that learns predictive rules from observation.

* **Potential Next Steps:**
  * **Establishing Standardized Benchmarks:** The community needs to move beyond single-task competitions to define a suite of benchmarks that assess the core capabilities of a virtual cell across multiple scales and modalities.
  * **Scaling Strategic Data Generation:** A coordinated effort, likely involving public-private partnerships, is needed to generate the massive, multimodal, and spatially-resolved datasets required for pre-training next-generation models.
  * **Integrating Causal Inference:** Developing novel AI architectures and training schemes that can move beyond learning correlations to infer and model causal relationships in biological networks.


## Breakout Session: Federated Future: Back to the Science of Discovery (Revvity Signals)

> David Gosalvez, PhD, Chief Strategy Officer, Revvity Signals
 
![](Media/28285.png) AI augmented discovery

federated learning

mode of operation, what does this company do, how do they do it, challenges addressed

personal thought on AI development in the field: 
- acceleration technological developments in research in industry
- despite the fast development, be pragmatic in its application



## The Rise of AI in Protein Design

> [GEN news de novo antibody design](https://www.genengnews.com/topics/artificial-intelligence/scratch-that-de-novo-antibody-design-enters-the-ai-drug-discovery-toolbox/)

**Panelists:**
* **Surge Biswas, PhD:** Co-founder and CEO, Nabla Bio
* **Tharindi Hapuarachchi, PhD:** Vice President, Platform Strategy and Operations, Generate:Biomedicines
* **Oliver Vance, PhD:** Co-founder, Basecamp Research

---

### Executive Summary

This panel discussion captures a pivotal moment in drug discovery, where AI has shifted the paradigm of protein engineering from mere prediction to active, *de novo* design. The panelists, representing three leading companies in the space, agree that the post-AlphaFold era is defined by the ability to programmatically design novel proteins with desired functions. They discuss how AI-designed proteins offer advantages over small molecules in terms of programmability, specificity, and pharmacokinetics. While celebrating the ability to now generate high-affinity binders from scratch, the panelists candidly identify the next frontier: designing for complex *in vivo* properties like manufacturability, immunogenicity, and specific biological function. The core of the discussion converges on the critical bottleneck and opportunity: **data**. The consensus is that public datasets have reached their limits, and the future of the field depends on proprietary, large-scale, and strategically generated data to train the next generation of multimodal foundation models, which will ultimately make drug development a truly "designable" process.

---

### The Legal Prelude on Patenting AI in Biotech

Before the main discussion, Tig Sheehan of Heslin Rothenberg Farley Mesiti (HRFM) provided a critical legal snapshot regarding the patentability of AI and biotech inventions in the U.S. This context is crucial for any company operating in the space.

#### The Underlying Problem: The *Mayo/Alice* Framework

For the last decade, U.S. patent law has been governed by a two-step test established by the Supreme Court cases *Mayo v. Prometheus* and *Alice v. CLS Bank*. This framework has made it exceptionally difficult to patent inventions in AI and diagnostics:

1. **Step 1: Is the invention "directed to" a patent-ineligible concept?** These concepts are laws of nature, natural phenomena, and abstract ideas. Courts have frequently ruled that core AI models are "abstract ideas" (mathematical algorithms) and that diagnostic methods are based on "laws of nature" (e.g., the correlation between a biomarker and a disease).
2. **Step 2: If so, is there an "inventive concept"?** The claim must contain an element that transforms it into something "significantly more" than the ineligible concept itself. This has been interpreted very narrowly, often invalidating patents that merely apply a concept using well-understood, routine, and conventional activities.

This framework has created significant uncertainty and has been a major hurdle for protecting innovations in personalized medicine, biomarker discovery, and the fundamental algorithms that power AI in drug design.

#### The Potential Solutions

Sheehan highlighted two developments signaling a major shift:

1. **The Patent Eligibility Restoration Act (PARA):** This bipartisan bill, if passed, would effectively abolish the *Mayo/Alice* framework. It would make all inventions eligible for patents unless they fall into a very narrow set of exceptions (e.g., an unmodified natural product). Crucially, it would clarify that inventions are not ineligible simply for using a mathematical formula or for containing elements that could be performed by the human mind. This would directly address the core issues hampering AI and diagnostic patents.
2. **USPTO Policy Shift:** The Director of the U.S. Patent and Trademark Office, Kathi Vidal (*note: the transcript incorrectly names her as John Squires*), has actively signaled support for broader patent eligibility. By issuing diagnostic method patents and testifying to Congress in strong support of PARA, the USPTO is indicating its desire for a change in the current regime.

#### The Strategic Takeaway

Given that patent examination can take years, Sheehan's advice was to **"skate to where the puck is going to be."** Innovators should file patent applications with a **"hedge" strategy**: include narrow claims that might survive the current strict *Mayo/Alice* test, but also include broad, commercially valuable claims that would become allowable if PARA passes. This ensures that some protection is likely, while preserving the opportunity for much stronger protection in the near future.

---

### Contextual Knowledge

* **Protein Design:** The rational design of new protein molecules to carry out specific functions. Historically, this was a trial-and-error process. AI aims to make it a predictive, engineering discipline.
* **AlphaFold:** A revolutionary AI model from Google DeepMind that solved the 50-year-old grand challenge of predicting a protein's 3D structure from its amino acid sequence with high accuracy.
* **De Novo Protein Design:** Designing a protein "from scratch" that is not an optimization of an existing, known protein. This allows for the exploration of a much wider range of structures and functions than is found in nature.
* **Foundation Model:** A large-scale AI model pre-trained on vast amounts of data. In this context, it would be a model pre-trained on massive biological datasets (sequences, structures, functions) that can be fine-tuned for specific design tasks.
* **Agentic AI:** AI systems that can autonomously reason, plan, and execute a series of actions to achieve a goal. In drug discovery, an agent could potentially integrate different models and data sources to manage a discovery program.
* **Developability:** A collective term for the properties a drug candidate must have to be successfully manufactured, formulated, and administered as a therapeutic (e.g., stability, solubility, low viscosity, non-immunogenicity).

---

### Delineation of Panel Discussion by Topic

The discussion progressed through six key themes, from the recent past to the long-term future of the field.

*(Note: The transcript contains minor name errors, such as "Therindy Haberarachi" for Tharindi Hapuarachchi. The corrected names are used here.)*

#### Topic 1: The Post-AlphaFold Transformation

The panel agreed that AlphaFold was a turning point that shifted the entire field's focus and mindset from prediction to design.

* **Surge Biswas (Nabla):** The field has moved from the problem of *predicting* a static 3D structure from a given sequence to the more powerful problem of *programmatically designing* the specific surface chemistry and shape of a protein to create novel functions and interactions.
* **Tharindi Hapuarachchi (Generate):** The biggest shift has been in **mindsets**. The realm of what is considered possible has expanded, leading to investment in true **multimodal models** that learn the mapping from `Sequence -> Structure -> Function` simultaneously. Furthermore, the rise of **agentic approaches** is democratizing access; a biologist can now use a natural language prompt (e.g., "Design an antibody to target X with property Y") to have an AI system orchestrate multiple models to generate candidates, a task that previously required a team of computational experts.
* **Oliver Vance (Basecamp):** AlphaFold was the **"starting gun"** that proved the AI playbook from other fields applies to biology. This playbook, defined by the **scaling laws** of AI (where predictable gains arise from scaling up data, model size, and compute), provides a compelling, technically feasible roadmap for achieving even greater breakthroughs.

#### Topic 2: The Case for Proteins as a Therapeutic Modality

The panelists articulated why AI-designed proteins are an attractive alternative to traditional small molecules.

* **Surge Biswas:** Proteins are **inherently programmable**. Their design space is discrete (a sequence of 20 amino acids), making it highly amenable to generative AI, unlike the continuous and complex chemical space of small molecules. Their larger size allows for more contact points with a target, leading to higher affinity (tighter binding) and specificity (fewer off-target effects), which are hallmarks of safer, more effective drugs.
* **Tharindi Hapuarachchi:** AI platforms are **generalizable**. The underlying architecture (e.g., a Transformer or Graph Neural Network) learns the fundamental "language" of protein biophysics. This means a single platform can be applied to design diverse protein types (antibodies, enzymes, cytokines), breaking down traditional silos of human expertise.
* **Oliver Vance:** Computers do not have the same **complexity ceiling** as human designers. A human can juggle a few design parameters at once. An AI model can, in principle, co-optimize a protein for hundreds of parameters simultaneously (affinity, specificity, stability, solubility, immunogenicity), navigating a high-dimensional design space that is beyond human intuition.

#### Topic 3: Augmenting the Drug Discovery Pipeline

The discussion focused on how AI is making the discovery process faster, cheaper, and more successful.

* **Tharindi Hapuarachchi:** Differentiated between two generative approaches: (1) **Optimization**, which makes incremental improvements to a known protein (akin to directed evolution), and (2) **De Novo design**, which generates entirely novel proteins from scratch, capable of producing new folds and functions.
* **Surge Biswas:** The ultimate vision is to make drug development **"designable"**—a shift from a process of *discovery* (screening random libraries) to one of *engineering* (specifying desired properties and generating a molecule that meets them). This increases the **clinical probability of success** by both finding better targets and designing better drugs.
* **Oliver Vance:** The move towards **foundation models** is critical. A model pre-trained on billions of natural proteins has already learned the implicit rules of folding and stability. This "prior experience" means it can be fine-tuned on very small, high-value clinical datasets with extreme data efficiency, a perfect setup for clinical translation where data is always scarce.

#### Topic 4: De Novo Design: Hype vs. Reality

The panel firmly positioned de novo design as a reality that is already delivering results, while being clear-eyed about the road ahead.

* **Surge Biswas:** De novo is here and working. Nabla's models are designing antibodies from scratch that bind challenging targets like GPCRs with **drug-quality, single-digit picomolar (pM) affinities**. The frontier is now designing for the multi-dimensional properties of **developability**, which requires generating new proprietary data on manufacturability, safety, and formulation.
* **Tharindi Hapuarachchi:** De novo is not hype, but there is a crucial distinction between designing a *protein* and designing a *therapeutic*. A de novo protein might be stable in a test tube but fail *in vivo* due to immunogenicity, rapid clearance, or aggregation. A "therapeutic" must satisfy these additional complex constraints.
* **Oliver Vance:** The progress is staggering. He posed a fundamental question in AI: will the next leap in controllability come from **explicitly modeling** molecular physics, or from **massive pre-training** on enormous datasets and letting the model learn the physics implicitly? The latter approach is currently favored in the broader AI community.

#### Topic 5: The Critical Role of Data

This was the core of the discussion, with a clear consensus that public data is insufficient and proprietary data is the key to competitive advantage.

* **Oliver Vance (Basecamp):** Public databases are a biased, piecemeal aggregation of historical experiments. Basecamp's strategy is to **rebuild from scratch by exploring global biodiversity** (e.g., in extreme environments). This uncovers proteins with novel folds and stability profiles, vastly enriching the "vocabulary" of the AI models trained on this data.
* **Tharindi Hapuarachchi (Generate):** Generate has built a rapid, closed **"design-build-test-learn" loop**. Their integrated wet/dry lab, with miniaturized assays and a Cryo-EM facility, allows the AI to design proteins, which are then physically created and tested, with the results immediately fed back as new training data. This allows the AI to iterate and improve in days or weeks.
* **Surge Biswas (Nabla):** Highlighted the trade-off between data **volume and relevance**. Nabla's strategy is a **co-evolution of AI and data**, using the AI as a "ratchet." The model is first trained on large, low-relevance data, then progressively fine-tuned on smaller, more precious, human-relevant datasets. This allows the model to incrementally "climb the ladder" towards understanding complex human biology.

#### Topic 6: Future Outlook: The Next 5-10 Years

The panelists shared ambitious visions for a future where AI transforms the very nature of drug discovery.

* **Tharindi Hapuarachchi:** The rise of **agentic tools** will democratize expertise. A single scientist will be able to query an AI agent that embodies the knowledge of an entire drug discovery organization, flattening the playing field and accelerating all phases of R&D.
* **Surge Biswas:** The goal is **"designable" drug development**. He is optimistic that within 5-10 years, it will be possible to identify the right biological target and then generate a human-ready drug at the push of a button.
* **Oliver Vance:** The focus will be on increasing the **sophistication** of what can be designed, moving beyond simple proteins to controllable protein-DNA complexes for cell and gene therapy. The ultimate goal is to design **cures**, where the AI can take in a patient's specific biological data and design a personalized, curative therapy in response.

---

### Comprehensive Final Summary

* **Motivation:** To transcend the slow, costly, and trial-and-error-based methods of traditional protein engineering. The goal is to leverage generative AI to create a new paradigm of protein design that is fast, predictive, and capable of producing novel therapeutics with a higher probability of clinical success.

* **Central Argument:** The panel argues that AI-driven protein design has matured from structure *prediction* to *de novo* design, marking a fundamental shift in the field. This new era is defined by a symbiotic relationship between generative AI models and massive, proprietary datasets. While the ability to design simple binders is becoming commoditized, the true competitive frontier and the key to unlocking transformative medicines lies in generating the right data to teach models how to design for complex *in vivo* functions and therapeutic properties.

* **Conclusion:** AI-powered protein design is a tangible reality that is already accelerating drug discovery programs. The future of the industry will be shaped by three converging forces: (1) the strategic generation of vast, diverse, and proprietary biological data; (2) the development of sophisticated, multimodal foundation models trained on this data; and (3) the integration of agentic AI to automate and optimize the entire discovery and development process. This trajectory points towards a future of "designable" medicines and highly sophisticated, potentially curative, therapies.

* **Current Limitations:**
  - **Designing for Complex Properties:** While designing for binding affinity is largely solved, designing for developability, manufacturability, non-immunogenicity, and specific *in vivo* behavior remains a major challenge.
  - **Data Scarcity for Relevance:** There is a critical lack of high-quality data directly relevant to human clinical outcomes, which is necessary to train models for the final steps of therapeutic design.
  - **Time Lag to Clinical Proof:** The long timelines of clinical trials mean that the true clinical impact of today's most advanced de novo design technologies will not be fully validated for several years.

* **Alternative Perspectives:** The discussion highlights different, but complementary, strategies for tackling the data problem. Basecamp's approach focuses on breadth by exploring nature's vast, untapped biodiversity. Generate and Nabla's approaches focus on depth by creating high-throughput, automated lab infrastructure to generate functional data for specific therapeutic problems.

* **Potential Next Steps:**
  - **Scaling Data Generation for *In Vivo* Properties:** A major industry focus will be on creating high-throughput assays that can generate data on manufacturability, immunogenicity, and other key therapeutic attributes.
  - **Building Multimodal Foundation Models:** Pre-training models on datasets that integrate sequence, structure, function, and *in vivo* data to create more holistic design platforms.
  - **Applying Agentic AI:** Deploying AI agents to manage the complexity of the discovery pipeline, from target selection to clinical trial design.
  - **Expanding to New Modalities:** Using the principles proven in protein design to tackle more complex challenges, such as designing sophisticated cell and gene therapies.

---
---
# Conference Analysis and Professional Development Advice (2025-11-01)

## Synergistic Report on "The State of AI in Drug Discovery 2025"

This conference provided a panoramic view of a field at an inflection point. The era of AI as a niche tool for isolated problems is over, replaced by a vision of integrated, data-driven engines powered by foundation models. Four major themes recurred across every session: the paradigm shift to generative and multimodal foundation models, the primacy of data strategy, the challenge of bridging the preclinical-to-clinical "translation gap," and the physical-world bottlenecks of biological R&D.

### Theme 1: The Foundation Model Paradigm Shift

The conference's central narrative was the triumph of the foundation model paradigm, marking a move from prediction to generation and from single-task tools to multimodal, general-purpose platforms.

*   **Synthesis of Views:** Bo Wang's presentation on scGPT and MedSAM served as a perfect case study, demonstrating how a single pre-trained Transformer architecture can be adapted to outperform a zoo of specialist tools in genomics and medical imaging. The Boltz-2 and Protein Design panels extended this concept into the molecular realm. They celebrated the post-AlphaFold shift from merely *predicting* structure to *designing* function. Speakers like Surge Biswas and Tharindi Hapuarachchi articulated how generative models are making protein therapeutics "programmable" and "designable," moving beyond nature's templates to create *de novo* binders with drug-like affinities. The "Virtual Cell" panel framed this as the ultimate goal: a suite of interconnected foundation models that predict cellular behavior across scales.

*   **Current State & Limitations:** The field has successfully built "GPT-2 level" foundation models for specific domains (single-cell genomics via scGPT, non-covalent binding via Boltz-2, protein backbones). However, these models are still largely correlational, not causal. As noted by Gabriele Corso and Bo Wang, they struggle with dynamic systems, allosteric sites, and require significant fine-tuning for new tasks or rare diseases. The biggest limitation, echoed by Najat Khan and Molly Gibson, is that excellence in one predictive dimension (e.g., binding affinity) does not guarantee a successful drug. The models do not yet capture the multi-parameter complexity of *in vivo* biology, such as PK/PD, toxicity, and immunogenicity.

*   **Conclusion & Future Development:** Foundation models are the new bedrock of computational biology. The path forward involves three key efforts:
    1.  **Scaling to "GPT-4":** Developing models with true zero-shot and reasoning capabilities, moving beyond correlation towards causality, as hinted by the BioReason project.
    2.  **Multimodality:** Building models pre-trained on truly multimodal data (e.g., integrating imaging, spatial omics, and proteomics as discussed by Emma Lundberg and Ron Alfa) to create a holistic understanding.
    3.  **Agentic Integration:** Creating AI agents that can intelligently orchestrate these foundation models, as envisioned by Tharindi Hapuarachchi, to automate the entire discovery pipeline from hypothesis to candidate.

### Theme 2: Data as the Decisive Asset

If foundation models are the engines, data is the fuel. A powerful consensus emerged that competitive advantage no longer lies in the model architecture, which is rapidly commoditizing, but in the data used to train it.

*   **Synthesis of Views:** The discussion presented a fascinating tension. Academics like Regina Barzilay passionately advocate for large-scale public data generation initiatives, akin to the PDB which enabled the AlphaFold revolution. In contrast, industry leaders like Najat Khan, Molly Gibson, and the entire Protein Design panel argued that the future is **proprietary, fit-for-purpose data**. Companies like Basecamp Research are exploring the breadth of nature's biodiversity, while Recursion, Generate:Biomedicines, and NOETIK are building automated labs to generate massive, deep datasets in-house, creating a closed "design-build-test-learn" loop. As Hani Goodarzi noted, we are in a new era where AI experts are now dictating the required scale and type of experimental data to biologists.

*   **Current State & Limitations:** The field has largely exhausted the utility of existing, fragmented public datasets. These datasets are often biased, "small" by AI standards, and lack the multimodality and direct human relevance needed to train next-generation models. The "Virtual Cell" panel was clear: the data required to model human patient biology simply does not exist and must be created. The primary limitation is the physical world—generating high-quality biological data is slow and expensive.

*   **Conclusion & Future Development:** The future of AI in drug discovery is a story of data strategy. The most successful organizations will be those that master the flywheel of AI-guided experimentation and data generation. Future progress depends on:
    1.  **Investing in Data Generation:** Building the automated robotic labs and human-relevant assay systems (e.g., organoids) that can generate data at the scale AI demands.
    2.  **Strategic Data Acquisition:** Focusing on data that closes the "translation gap"—perturbation data, spatial data, and data on "developability" properties (manufacturing, toxicity, etc.).
    3.  **New Collaboration Models:** Exploring pre-competitive consortia and federated learning approaches, as mentioned by Stacie Colad-Thomson, to share insights from proprietary data without revealing the data itself.

### Theme 3: Bridging the "Translation Gap"

A soberingly pragmatic theme was the chasm between preclinical AI success and clinical failure. Discovering a potent molecule is only the first, and perhaps easiest, step.

*   **Synthesis of Views:** Derek Lowe acted as the panel's conscience, reminding everyone that AI's impact is inversely correlated with the problem's importance; it excels at well-defined, preclinical tasks but struggles with the messy, complex biology that causes clinical failures (e.g., predictive toxicology). Molly Gibson powerfully articulated that the entire field's valuation hinges on solving this. Her "billion-dollar question" answer was unequivocal: invest in getting AI-designed drugs through human trials to prove they have a higher probability of success. This sentiment was echoed by Najat Khan, who identified predicting PK/PD and human dose as the next "huge unlock," and Ron Alfa, whose work at NOETIK starts with human pathology data to stay anchored to patient reality.

*   **Current State & Limitations:** The industry has a "last mile problem." AI can accelerate the journey to a drug candidate, but over 90% of drugs still fail in the clinic. This is because our fundamental understanding of human biology is incomplete, and the data from these failures is rarely published, starving models of crucial negative examples. Experimental models (cell lines, animals) are poor proxies for human disease, a ceiling that Hani Goodarzi believes in-silico models can eventually break.

*   **Conclusion & Future Development:** Closing the translation gap is the industry's grand challenge. Success requires a multi-pronged attack:
    1.  **AI for Clinical Trials:** Applying AI not just to discovery but to optimize clinical trial design, patient stratification, and biomarker selection.
    2.  **Better Experimental Models:** Investing in more human-relevant assays (organoids, patient-derived tissues) to generate data that is more predictive of clinical outcomes.
    3.  **Data Feedback Loops:** Creating infrastructure to feed clinical and real-world data back into the discovery models, creating a learning loop that spans the entire R&D process.

### Conference Conclusion: Key Messages

The "State of AI in Drug Discovery 2025" conference painted a picture of a field rapidly maturing past the initial hype cycle. The central message is that AI is transitioning from a tool for discovery to a platform for **engineering**. The era of siloed, predictive models is giving way to integrated, generative foundation models that can design novel biology. However, this vision is entirely dependent on a parallel revolution in the physical world: the strategic, large-scale generation of proprietary, multimodal, human-relevant data through lab automation. The ultimate success of this entire enterprise will be measured not by the speed of preclinical discovery, but by a tangible improvement in the clinical probability of success, a goal that remains the field's most formidable challenge.

---

## Skills for the Modern AI-Focused Bioinformatician

The conference makes it clear that the role of a bioinformatician is evolving from a data analyst into a "full-stack" biological problem solver. To thrive, you must move beyond simply using tools and learn to build, integrate, and strategize.

### Critical Technical Skills to Acquire

1.  **Master Foundation Model Architectures:** Don't just use them, build them. Deeply understand the Transformer architecture, including attention mechanisms, tokenization strategies for biological data (like in scGPT), and generative approaches (like diffusion and autoregressive models). Go through the code of models like Boltz-2, scGPT, and MedSAM on GitHub.
2.  **Embrace Multimodality:** Your expertise in single-cell, metabolomics, and genomics is a great start. The future is integrating these. Gain hands-on experience with spatial transcriptomics and proteomics data, and more importantly, with computational methods that fuse these modalities with imaging and sequence data.
3.  **Become a "Data-First" Thinker:** Learn to think like the panelists from NOETIK and Generate. Understand that the model is only as good as the data. Develop skills in experimental design, data curation, and quality control. Learn how to identify the biases in public datasets and articulate what "fit-for-purpose" data would look like for a specific biological question.
4.  **Develop MLOps & Engineering Acumen:** It's not enough to write a script that works once. Learn how to build robust, scalable, and reproducible data pipelines. Master tools like Docker, Nextflow or Snakemake, and gain proficiency in cloud computing (AWS, GCP), as pre-training foundation models is computationally expensive. Your AWS Cloud Practitioner certification is a good first step; now go deeper.
5.  **Get Your Hands on Hardware (Figuratively):** The "design-build-test-learn" loop is powered by lab automation. While you don't need to be a robotics engineer, you should understand the principles and data output of automated microscopy, liquid handlers (like the Beckman Echo), and high-throughput screening. This will allow you to design computational workflows that integrate seamlessly with the physical lab.

### Essential Soft Skills for a New Era

1.  **Become a Translator:** The most valuable computational scientists are those who can bridge the gap between domains. You must be able to listen to a biologist describe a problem, translate it into a well-defined computational task, and then explain the results (and the model's limitations) back to them in an intuitive way. As Derek Lowe and Molly Gibson emphasized, integrated teams of experts are non-negotiable.
2.  **Develop Product & Project Mentality:** Shift from thinking about "running an analysis" to "building a solution." Your experience developing Shiny and Streamlit apps is excellent. Frame your projects not as scripts, but as products for other scientists. This requires user-centric thinking, clear documentation, and project management skills to deliver a useful tool on a timeline.
3.  **Cultivate Pragmatic Skepticism:** As Derek Lowe's contributions showed, the hype is always ahead of reality. Learn to critically evaluate new AI methods. Ask the hard questions: What are the limitations? How was it validated? Does it work on real-world, messy data, or just a clean benchmark? Will this actually solve a problem that matters to drug development? This critical mindset is essential for navigating the field and making sound technical decisions.
4.  **Embrace a Collaborative, Open-Source Ethos:** The success of Boltz-2 and MedSAM was driven by their open-source nature. Contribute to open-source projects. Participate in community challenges like the "Virtual Cell Challenge." This not only builds your skills and public profile but also plugs you into the collaborative network that is driving the science forward.

---

## Personalized Professional and Academic Advice

Your background and current thesis project place you squarely at the center of the most exciting trends discussed at this conference. You have a strong, multimodal foundation in both omics and programming, and your thesis is a microcosm of the grand challenges in the field. Here is critical, actionable advice to leverage this position.

### Professional Development: From Student to Expert

1.  **Go Deeper on Your Thesis Models:** Your plan to use Omnipose and SAM is excellent. Don't just be a *user*. Your goal should be to become a local expert on these architectures. Read the original papers for the Vision Transformer (ViT) and the architectures behind Omnipose. Try to re-implement a simplified version in PyTorch. This deep understanding is what separates a technician from a machine learning scientist.
2.  **Frame Your Thesis as a "Virtual Cell" Problem:** Your project is not just "image segmentation." You are building a multimodal model to understand the dynamics of host-pathogen interactions. You are integrating imaging (morphology), spatial data (smFISH localization), and time-series analysis (tracking). When you write your thesis and talk about your work, use this language. You are building a small-scale, data-driven model to predict cellular behavior in response to stimuli (host interaction)—this is the very definition of the "virtual cell" discussed by the panel.
3.  **Create Your Own "Fit-for-Purpose" Data:** Your proposal mentions manual labeling to create a gold-standard dataset. This is *exactly* the "proprietary data generation" that industry leaders are talking about. Document this process meticulously. This experience is incredibly valuable and demonstrates that you understand the "data-first" principle. It is a key selling point for your resume.

### Career Choice: The "Tech-Bio" Sweet Spot

Your profile is a perfect fit for the new breed of "tech-bio" companies. These are not traditional pharma companies with a small bioinformatics group, nor are they pure tech companies that don't understand biology. They are integrated companies built from the ground up around the "design-build-test-learn" flywheel.

*   **Your Ideal Role:** Look for titles like "Machine Learning Scientist," "Computational Biologist," or "AI Scientist" at companies like **Recursion, Generate:Biomedicines, Xaira Therapeutics, Nabla Bio, or NOETIK**. These roles will leverage your dual expertise in biology and cutting-edge AI. Your experience with both omics and imaging makes you a strong candidate for teams focused on multimodal learning.
*   **Academia vs. Industry:** The lines are blurring. An academic lab like Regina Barzilay's at MIT or a research hub like the Arc Institute operates with the resources and ambition of a startup. If you choose academia, seek out these highly collaborative, well-funded environments. If you choose industry, target the R&D-centric tech-bio companies where you can still publish and engage with the scientific community. Avoid roles where you would be siloed into just running routine analysis pipelines.

### PhD Program Choice and Application Strategy

Your master's thesis is the perfect springboard for a top-tier PhD. Your application needs to tell a compelling story that connects your project to the future of the field.

1.  **Target the Right PIs:** Look for labs that are not just *applying* AI but are *building* the next generation of models for biology. Based on the conference, your ideal PI would be working on:
    *   **Multimodal Foundation Models:** Integrating imaging with genomics/proteomics.
    *   **Generative Models for Biology:** Designing sequences, structures, or cellular behaviors.
    *   **Spatial Omics & Systems Biology:** Using spatial data to model tissue-level emergent properties.
    *   **Look for PIs who are speakers at these conferences or who publish in journals like *Nature Methods* or *Nature Biotechnology* on new computational techniques.** Think of the labs of Bo Wang (now at Xaira, but his academic lineage), Emma Lundberg (spatial proteomics), or Hani Goodarzi (causal biology/RNA).

2.  **Crafting Your Application Narrative:**
    *   **Statement of Purpose:** Do not just list your skills. Tell a story. Start with the grand challenge: understanding complex biological systems like host-pathogen interactions is limited by our ability to analyze dynamic, multimodal data at scale. Frame your thesis project as your first attempt to solve this challenge.
    *   **Connect Your Experience to Their Work:** Explicitly state how your work on *C. albicans* segmentation and tracking is a direct application of the principles of building data-driven, predictive models of cellular systems. Mention your experience in creating a high-quality labeled dataset as evidence of your understanding of the "data bottleneck."
    *   **Show, Don't Just Tell:** Your GitHub is a powerful asset. Make sure the repositories for your `isotopeApp` and `rfApp` are clean, well-documented, and showcase your ability to build user-friendly tools. This is tangible proof of the "engineering and product mindset" that is so valuable.

Your current trajectory is excellent. The key is to now consciously and strategically frame your skills and experience in the language of the modern AI-driven biotechnology revolution. You are not just a bioinformatician; you are an architect of the virtual cell.