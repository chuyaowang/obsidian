# Genome-wide transposon insertion sequencing

A **genome-wide transposon insertion sequencing (TIS)** screen—often referred to as Tn-seq, INSeq, or TraDIS—is a powerful, high-throughput functional genomics technique. It allows researchers to determine the function and importance of nearly every gene in a microorganism's genome in a single massive experiment. 

Here is a breakdown of what it is, what it measures, and how it works. 

### What does a TIS screen measure?
Fundamentally, TIS measures **gene fitness and essentiality**. 

It answers the question: *How important is a specific gene for this organism's survival under a specific condition?* By comparing a bacterial population before and after exposure to a stressor (like an antibiotic, starvation, or an immune system response), researchers can measure:
* **Essential genes:** If a gene is absolutely required for survival, any bacteria with a mutation in that gene will die.
* **Conditionally essential genes:** Genes that are only needed under specific conditions (e.g., a gene needed to digest lactose is only essential if lactose is the only food source).
* **Detrimental genes:** Genes whose disruption actually gives the bacteria a survival advantage in a specific environment.

### How does it work? 
The brilliance of TIS lies in treating a population of millions of bacteria as a giant, pooled competition assay. The process happens in four main steps:

**1. Generating the Mutant Library (Mutagenesis)**
Researchers introduce a "transposon" into a large population of bacteria. A transposon is a piece of DNA—often called a "jumping gene"—that can insert itself randomly into the host's genome. 
* When the transposon lands inside a gene, it disrupts that gene, effectively breaking it (creating a "knockout").
* The goal is to create a saturated library: a pool of millions of bacteria where the transposon has landed in every conceivable location across the genome. Ideally, every non-essential gene is broken in at least one bacterium in the tube.

**2. The Competition (Selection/Screening)**
The mutant library is split into two groups:
* **Control group:** Grown in a standard, happy environment.
* **Test group:** Grown in the environment of interest (e.g., inside a macrophage, or in a medium lacking a specific nutrient).
The bacteria compete to survive and reproduce. If a transposon broke a gene that a bacterium needed to survive the test environment, that specific mutant dies off and is lost from the population.

**3. Sequencing (Finding the Transposons)**
After the competition, researchers extract the genomic DNA from the surviving populations. They use molecular scissors (restriction enzymes) and specialized primers to amplify only the exact junctions where the transposon DNA meets the bacterial genomic DNA. They then use Next-Generation Sequencing (NGS) to read millions of these junctions.

**4. Mapping and Counting (Bioinformatics)**
The DNA sequences are mapped back to the organism's reference genome to identify exactly where every transposon landed. 
* **The read count acts as a barcode.** If a gene has thousands of transposon reads in the control group but zero reads in the test group, it means mutants with a broken version of that gene died. Therefore, that gene was essential for surviving the test condition.
* Conversely, if a gene has significantly *more* reads in the test group than the control, breaking that gene somehow made the bacteria fitter and more successful. 

In short, TIS is a sophisticated game of biological process-of-elimination, allowing scientists to map the functional landscape of an entire genome in one go.