# Precision Medicine through AI, Genomics, and Metagenomics

> Dr. Ana Tereza Ribeiro de Vasconcelos, Head of the Bioinformatics Laboratory, National Laboratory for Scientific Computing LNCC/MCTI Brazil

### Logical Flow and Section-by-Section Summary

The presentation is divided into three main parts, following an introduction to the speaker's institution and its capabilities. It showcases specific research projects in metagenomics before moving to the main topic: a large-scale AI platform for precision medicine.

#### 1. Introduction: The Lab and its Mission

*   **Summary:** The speaker introduces their institution, the National Laboratory for Scientific Computing in Brazil, which is the largest supercomputer center for scientific work in Latin America. The lab combines a wet lab for sequencing (genomes, transcriptomes, metagenomes) with the massive computational power of the "Santos Dumont" supercomputer. Their work spans virus surveillance (SARS-CoV-2, Zika, etc.), precision medicine, the "One Health" concept, and biotechnology, with a focus on Brazilian biodiversity and health.
*   **Transition:** The speaker narrows this broad overview to focus on two key areas of recent work: metagenomics and precision medicine, starting with two PhD student projects in metagenomics.

#### 2. Project Showcase Part 1: Metagenomics for Antibiotic Resistance and Sporulation

*   **Challenge Resolved:** 
    1.  To understand the distribution of antibiotic resistance genes across the vast and diverse regions of Brazil.
    2.  To identify and classify unknown bacteria from metagenomic data, specifically those with the ability to form spores (a dormant, resilient state that can be pathogenic).
*   **Methods Used:**
    1.  **Resistance Mapping:** Large-scale metagenomic sequencing of samples from cows, poultry, humans, and swine from different parts of Brazil. The data was used to assemble Metagenome-Assembled Genomes (MAGs).
    2.  **Sporulation Classification:** A machine learning classifier was developed. It was trained on the genomic features of known sporulating and non-sporulating bacteria and used a stacking ensemble approach to improve accuracy.
*   **Results:**
    1.  The study successfully mapped antibiotic resistance across Brazil and identified new resistance genes. However, it also revealed a large amount of microbial "dark matter" (genomes that could not be fully identified).
    2.  The machine learning model was able to infer and identify novel sporulating bacterial species within this "dark matter," some of which were shared across different host species (e.g., humans and cows).
*   **Transition:** The talk moves from the challenges of bacterial metagenomics to another complex metagenomics problem: identifying viruses, which have smaller and more fragmented genetic signatures.

#### 3. Project Showcase Part 2: Metagenomics for Viral Discovery

*   **Challenge Resolved:** Identifying novel viruses from metagenomic (specifically, metatranscriptomic) data is difficult because the genetic fragments (reads) are often too short for traditional alignment-based tools to work effectively.
*   **Methods Used:** The lab developed an alignment-free feature extraction method called **(m,n)-MER**, a variation of the k-mer counting strategy. This method was optimized for short sequences and packaged into a user-friendly workflow named **Morvir** (available on GitHub).
*   **Results:** The (m,n)-MER method demonstrated superior performance compared to traditional k-mer approaches on short fragments (300-1,000 base pairs). By applying the (m,n)-MER workflow to mosquito metatranscriptome data, the team identified **over 600 previously undescribed mosquito-associated viruses**.
*   **Transition:** Having demonstrated their expertise in handling complex 'omics data with custom computational tools, the speaker shifts to the main focus of the talk: applying similar principles to the even larger challenge of human precision medicine.

#### 4. Core Topic: An AI Platform for Precision Medicine

*   **Challenge Resolved:** How to enable the analysis and interpretation of a massive national dataset (30,000 Brazilian genomes) for researchers who may not be bioinformatics experts. A critical part of this challenge is ensuring the output is scientifically accurate and avoids the "hallucination" (fabricated information) common in general-purpose AI models.
*   **Methods Used:** The team is building a sophisticated AI platform with a **Retrieval-Augmented Generation (RAG)** architecture. Key features include:
    1.  **Curated Knowledge Base:** The platform's models are trained and informed *only* by a knowledge base constructed from scientific literature, not the open internet.
    2.  **RAG Engine:** When a user asks a question, the system first retrieves relevant, verified information from its knowledge base and then uses a Large Language Model (LLM) to generate a scientifically accurate, context-aware, and referenced answer.
    3.  **Integrated Analysis:** The platform includes built-in pipelines to process user-submitted data (like VCF or BAM files), allowing for direct analysis.
    4.  **User Interface:** The platform will be accessible via a chatbot and an API.
*   **Results:** The platform is designed to be a free resource for Brazilian researchers. It can take user queries and return answers as text, tables, or gene lists, complete with references to the supporting scientific articles. It is currently being piloted in a collaborative project on neurodegenerative diseases (ALS, Alzheimer's, Parkinson's) to identify important structural variants from patient exomes and genomes.
*   **Transition:** The presentation concludes with a summary of the importance of collaboration, followed by a Q&A session.

### Q&A Session

*   **Question 1 (Data Privacy):** How will the platform handle the privacy of the sensitive 'omics data that users upload?
    *   **Answer:** All data will be encrypted. Furthermore, in its initial phase, access to the platform will be restricted to researchers affiliated with government institutions in Brazil to ensure a controlled and secure environment.

*   **Question 2 (Viral Diagnostics):** A researcher from Nigeria working on viral hemorrhagic fevers (like Zika, Dengue) asked if there is a universal DNA sequence for this group of viruses to design a multiplex PCR diagnostic tool.
    *   **Answer:** Yes, specific sequences for these viruses exist, and commercial kits (e.g., from Illumina) are available for this purpose. The speaker offered to share more detailed information via email.

*   **Question 3 (Data Normalization):** How do you normalize and ensure quality control for data coming from many different sources (your lab, other databases, past research papers) that may use different experimental methods?
    *   **Answer:** The data from scientific papers is not used for direct sequence-level comparison but rather to **build the knowledge base for annotation**. For example, the platform uses information from papers to know which genetic variants have been previously associated with a disease, regardless of the sequencing method used. This information is then used to annotate the new data generated by the user or the project.

### Comprehensive Summary

*   **Motivation:** The rapid increase in the scale of genomic and metagenomic sequencing, exemplified by Brazil's national project to sequence 30,000 genomes, has created a critical need for powerful, accessible, and reliable analysis tools to translate this data into clinical insights for precision medicine.

*   **Central Argument:** The speaker argues that while computational analysis is key, general-purpose AI models are not suitable for clinical genomics due to their propensity for "hallucination." The solution is a specialized AI platform built on a **Retrieval-Augmented Generation (RAG) architecture**. By grounding the AI's responses in a curated, firewalled knowledge base derived exclusively from scientific literature, the platform can provide accurate, verifiable, and context-aware genomic interpretations, effectively democratizing advanced bioinformatics for a wider research community.

*   **Conclusion:** The research group has demonstrated its capability by creating novel computational methods for complex metagenomic analyses. They are now leveraging this expertise to build a powerful AI-driven platform that will serve as critical infrastructure for Brazil's precision medicine initiatives. The project highlights a global shift towards using curated AI to manage the data deluge in biomedical research, emphasizing that collaboration and specialized tool-building are essential for progress.

*   **Potential Next Steps:** The immediate next step is to complete the pilot phase of the AI platform with the neurodegenerative disease data. Following that, the platform will be rolled out to the broader Brazilian research community to analyze data from the 30,000-genome project and other studies. In the long term, it may be made available to the international community. Continued development will involve expanding the knowledge base and refining the analysis engines.