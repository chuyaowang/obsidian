# Gene Expression Regulation

- How much proteins are expressed from a gene
- [Transcription Regulation](Transcription%20Regulation.md)
- RNA processing control
- RNA transport and localization
- RNA degradation
- Translation control
- Protein activity control

## Transcription level control

See [Lac Operon](Lac%20Operon.md)

Activator protein increases affinity of sigma factors with the sequence.
Repressor prevents RNA polymerase from binding to the promoter

## Post-transcription control

### Guanine Riboswitches

In the context of a **riboswitch**, guanine can serve as a **ligand** that binds to a specific region of the riboswitch, triggering changes in gene expression. Riboswitches are regulatory segments of mRNA that can directly bind small molecules (like metabolites) without the need for proteins, influencing the expression of the genes encoded by the mRNA.

#### Guanine's Role in a Riboswitch:

1. **Ligand Binding**: In a **guanine-sensing riboswitch**, guanine binds to a specific aptamer domain in the riboswitch, which is usually located in the 5' untranslated region (UTR) of the mRNA. This aptamer domain is highly specific for guanine and can distinguish it from other purines like adenine.

2. **Structural Changes**: When guanine binds to the aptamer domain, it induces a conformational change in the mRNA structure. Riboswitches typically have two structural domains:
   - **Aptamer domain**: Binds the guanine.
   - **Expression platform**: Undergoes conformational changes to control gene expression.
   
   Upon guanine binding, the secondary structure of the mRNA shifts, which can either:
   - **Terminate transcription**: By forming a transcriptional terminator hairpin, preventing RNA polymerase from transcribing downstream genes.
   - **Block translation**: By sequestering the ribosome-binding site, preventing the ribosome from translating the mRNA.

3. **Regulating Purine Metabolism Genes**: Guanine riboswitches typically control genes involved in purine biosynthesis or transport. When guanine levels are high, the riboswitch binds guanine and downregulates the expression of genes responsible for producing or importing guanine, conserving cellular resources.

#### Example:

In *Bacillus subtilis*, the **guanine riboswitch** controls the expression of genes related to purine metabolism. When intracellular guanine concentrations are high, guanine binds to the riboswitch, halting further transcription of the purine biosynthesis genes. When guanine levels are low, the riboswitch remains in a conformation that allows transcription and subsequent translation of the necessary genes.

In summary, guanine in a riboswitch acts as a regulatory signal that binds to the riboswitch's aptamer domain, leading to structural changes that control gene expression based on the cell's need for guanine.

### RNA Interference

**RNA interference (RNAi)** is a biological process in which small RNA molecules silence the expression of specific genes by degrading mRNA or inhibiting its translation. The main small RNA molecules involved are [Small Interfering RNA](Small%20Interfering%20RNA.md) and [microRNA](microRNA.md). Here's an overview of the key steps in the RNAi pathway:

#### 1. dsRNA Recognition and Processing by Dicer:
   - **Trigger**: The process starts with the presence of **double-stranded RNA (dsRNA)** or **pre-miRNA** in the cell. This can be introduced by viral infection, transposons, or artificially (in the case of siRNA), or naturally transcribed (in the case of miRNA).
   - **Dicer Enzyme**: The enzyme **Dicer**, an RNase III endonuclease, recognizes and cleaves the dsRNA or pre-miRNA into small double-stranded RNA fragments. These fragments are typically:
     - **siRNA**: ~21-23 nucleotides long with 2-nucleotide overhangs on the 3' end.
     - **miRNA**: Also processed from precursor miRNA (pri-miRNA) into ~21-23 nucleotide mature miRNA molecules.

#### 2. Formation of the RNA-Induced Silencing Complex (RISC):
   - After processing by Dicer, one strand of the small RNA fragment (the **guide strand**) is incorporated into the **RNA-induced silencing complex (RISC)**.
   - The other strand, known as the **passenger strand**, is typically degraded.
   - The RISC complex includes core proteins such as **Argonaute** proteins, which are essential for gene silencing activity.

#### 3. Target mRNA Recognition:
   - The **guide strand** within the RISC serves as a template to recognize complementary or partially complementary sequences in target mRNA molecules.
     - **siRNA**: Perfectly complementary to its target mRNA, leading to precise targeting.
     - **miRNA**: Partially complementary to the target, typically binding to the 3' untranslated region (UTR) of mRNA, leading to more general regulation.

#### 4. Gene Silencing:
   Once the RISC complex binds to the target mRNA, two possible outcomes occur based on the level of complementarity between the guide strand and the mRNA:
   
   - **mRNA Cleavage and Degradation**:
     - **siRNA mechanism**: When the base-pairing between the siRNA guide strand and the mRNA is perfect or near-perfect, the **Argonaute protein** within RISC cleaves the target mRNA in the middle of the complementary region.
     - This cleavage leads to **mRNA degradation** by cellular exonucleases, preventing translation of the mRNA into protein.

   - **Translational Repression and/or mRNA Destabilization**:
     - **miRNA mechanism**: When the base-pairing between the miRNA guide strand and the mRNA is **imperfect** (typically with miRNA), RISC does not cleave the mRNA but instead:
       - **Blocks translation**: RISC prevents the ribosome from translating the mRNA into protein.
       - **Promotes mRNA destabilization**: The mRNA may be directed to processing bodies (**P-bodies**) for degradation, reducing mRNA stability over time.

#### 5. Gene Silencing Outcome:
   - **siRNA pathway**: Leads to **degradation** of the target mRNA, completely preventing protein synthesis.
   - **miRNA pathway**: Leads to **translational repression** or **mRNA destabilization**, reducing but not entirely eliminating protein synthesis.

### Bistable/bimodal gene regulation