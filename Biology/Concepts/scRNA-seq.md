# scRNA-seq

## Steps

### 1. Sample Preparation

#### A. Cell Isolation
- **Tissue Dissociation**: If starting from a tissue sample, the tissue must be dissociated into a single-cell suspension. This can be done using enzymatic digestion (e.g., collagenase, trypsin) and mechanical dissociation (e.g., pipetting, using a tissue dissociator).
- **Cell Sorting**: Cells are often sorted to ensure a pure population of viable cells. Fluorescence-activated cell sorting (FACS) or magnetic-activated cell sorting (MACS) can be used.

#### B. Viability Assessment
- **Cell Viability Staining**: Use dyes such as Trypan Blue or propidium iodide to assess and ensure that only live cells are processed further.

### 2. Cell Capture and Barcoding

#### A. Droplet-based Methods (e.g., 10x Genomics Chromium)
- **Encapsulation**: Individual cells are encapsulated into droplets along with barcoding beads. Each bead is coated with oligonucleotides containing a **unique cell barcode**, a **unique molecular identifier (UMI)**, and a **poly(T) sequence** to capture polyadenylated mRNA.
- **Reverse Transcription**: Inside each droplet, reverse transcription occurs, where the poly(T) sequence binds to the poly(A) tail of mRNA, and the barcode and UMI are incorporated into the **cDNA**.

#### B. Well-based Methods (e.g., Smart-seq2)
- **Cell Sorting into Wells**: Single cells are sorted into individual wells of a microplate.
- **Lysis and Reverse Transcription**: Cells are lysed, and mRNA is reverse transcribed into cDNA using oligo(dT) primers with a unique barcode and UMI sequence.

#### C. Combinatorial Indexing (e.g., SPLiT-seq)
- **Split-Pool Barcoding**: Cells are split into multiple wells, each well receiving a unique barcode. Cells are then pooled and split into wells again, receiving a second barcode. This process is repeated several times to generate unique combinations of barcodes for each cell.

### 3. cDNA Amplification

- **PCR Amplification**: The barcoded cDNA is amplified by _PCR_. This step increases the quantity of cDNA for downstream applications.

### 4. Library Preparation

- **Fragmentation and Size Selection**: Amplified cDNA is _fragmented_ to appropriate sizes (typically 200-500 bp) and size-selected to ensure uniformity.
- **Adapter Ligation**: _Sequencing adapters_ are ligated to the ends of the cDNA fragments. These adapters are necessary for attaching the cDNA to the sequencing flow cell.
- **Library Amplification**: Another round of PCR may be performed to amplify the library, incorporating _sample-specific barcodes_ if multiplexing.

### 5. Sequencing

- **High-throughput Sequencing**: The prepared **cDNA library** is sequenced using high-throughput sequencing platforms such as Illumina's NovaSeq or HiSeq. During sequencing, both the **cell barcodes, UMIs, and RNA sequences** are read.

### 6. Data Processing and Analysis

#### A. Base Calling and Demultiplexing
- **Base Calling**: Converts raw sequencing data into nucleotide sequences.
- **Demultiplexing**: Assigns each read to its originating cell based on the cell-specific barcodes.

#### B. Read Alignment
- **Quality Control**: Filters out low-quality reads and adapters.
- **Alignment**: Maps the reads to a reference genome or transcriptome to determine the origin of each RNA fragment.

#### C. UMI Deduplication
- **UMI Counting**: Counts the number of unique UMIs associated with each gene to estimate the number of unique RNA molecules, removing PCR duplicates.

> [!note] Deduplication
> During PCR, each original RNA/cDNA molecule is amplified to many copies, so does the UMI associated with each of them. Deduplication makes sure each original molecule is only counted once. A highly expressed genes will be in many [mRNA](mRNA.md) transcripts, or high UMI count.

#### D. Normalization and Batch Correction
- **Normalization**: Adjusts UMI counts to account for differences in sequencing depth and other technical variations.
- **Batch Effect Correction**: Removes technical variability introduced by different experimental batches.

#### E. Downstream Analysis
- **Gene Expression Analysis**: Identifies and quantifies gene expression levels for each cell.
- **Clustering and Dimensionality Reduction**: Groups cells based on similar gene expression profiles and reduces data dimensions using methods like PCA, t-SNE, or UMAP.
- **Differential Expression**: Identifies genes that are differentially expressed between cell clusters or conditions.
- **Cell Type Identification**: Assigns cell types based on known marker genes or through comparison with reference datasets.

### Summary of scRNA-seq Workflow

1. **Sample Preparation**: Isolate single cells from the sample.
2. **Cell Capture and Barcoding**: Encapsulate cells and add unique barcodes and UMIs.
3. **cDNA Amplification**: Amplify barcoded cDNA.
4. **Library Preparation**: Fragment, size-select, and ligate adapters to cDNA.
5. **Sequencing**: Sequence the cDNA library.
6. **Data Processing and Analysis**: Process raw data, align reads, deduplicate UMIs, normalize, correct batch effects, and perform downstream analyses.

By following these steps, researchers can obtain high-resolution gene expression profiles at the single-cell level, enabling the study of cellular heterogeneity and gene expression dynamics in complex biological systems.

## Read depth

Read depth, also known as sequencing depth or coverage, refers to the number of times a specific nucleotide in the genome or transcriptome is sequenced during an RNA sequencing (RNA-seq) experiment. It is a crucial metric in sequencing studies and has significant implications for the accuracy and reliability of the data.

### Read Depth in RNA-Seq

1. **Definition**:
    
    - Read depth is the average number of sequencing reads that align to a particular region of the genome or transcriptome. It is typically expressed as "X-fold coverage" (e.g., 10x, 50x), where "X" indicates the average number of reads covering each nucleotide.
2. **Importance**:
    
    - **Accuracy**: Higher read depth increases the accuracy of detecting RNA molecules, reducing the likelihood of missing low-abundance transcripts.
    - **Quantification**: Adequate read depth ensures more reliable quantification of gene expression levels, particularly for genes expressed at low levels.
    - **Variant Detection**: In genomic studies, higher read depth improves the ability to detect single nucleotide polymorphisms (SNPs) and other genetic variants.
    - **Error Reduction**: Higher coverage helps to average out sequencing errors and biases, leading to more robust data.
3. **Determining Optimal Read Depth**:
    
    - The optimal read depth depends on the goals of the study, the complexity of the transcriptome, and the expected expression levels of genes.
    - For standard RNA-seq studies, typical read depths range from 10-30 million reads per sample. For more comprehensive studies, such as those aiming to detect low-abundance transcripts or rare variants, deeper sequencing might be required.
4. **Balancing Cost and Depth**:
    
    - Higher read depth generally leads to more accurate data but also increases sequencing costs. Researchers need to balance the desired depth with available budget and the specific requirements of their study.

### Practical Example

In a single-cell RNA sequencing (scRNA-seq) experiment, achieving sufficient read depth is particularly important due to the low amount of starting material and the inherent variability between individual cells. In such cases, a high read depth ensures that even low-abundance transcripts are detected and quantified accurately, providing a more comprehensive view of the cellular transcriptome.

## UMIs

Unique Molecular Identifiers (UMIs) are designed to be unique for each RNA molecule through the incorporation of random nucleotide sequences during the preparation of RNA-seq libraries. Here’s how UMIs are made to ensure their uniqueness:

1. **Random Sequence Generation**:
   - UMIs are typically short sequences, often 6-12 nucleotides long, that are composed of random nucleotides (A, T, C, G). 
   - The randomness of the sequence ensures a high diversity of UMIs. For example, a 10-nucleotide UMI can theoretically generate $4^{10} = 1,048,576$ unique combinations.

2. **Incorporation into Primers**:
   - During the RNA library preparation, the UMI sequences are incorporated into the primers used for reverse transcription or during the initial amplification step.
   - These primers attach to each RNA molecule and include a random UMI sequence at a specific location.

3. **Attachment to RNA Molecules**:
   - Each RNA molecule is tagged with a unique UMI as it is reverse-transcribed into cDNA. This tagging is done before any amplification steps, ensuring that each original RNA molecule has a distinct UMI.

4. **Sequencing and Data Analysis**:
   - During sequencing, both the cDNA and its associated UMI are sequenced together.
   - In data analysis, reads are grouped by their UMI sequences, allowing for the identification and counting of unique RNA molecules.

### Ensuring Uniqueness and Reducing Collisions

1. **Sufficient UMI Length**:
   - The length of the UMI is chosen to provide a high number of unique combinations, significantly reducing the probability of two different RNA molecules receiving the same UMI (a collision).

2. **Randomness Verification**:
   - Quality control steps can verify the randomness and distribution of UMIs. Non-random distribution might indicate issues with the synthesis of UMIs or biases in the library preparation process.

3. **Error Correction**:
   - During data analysis, error correction algorithms can help to distinguish true UMIs from those altered by sequencing errors, further ensuring the accuracy of UMI-based quantification.

In summary, UMIs are made unique for each RNA molecule by incorporating random nucleotide sequences into primers used during library preparation. The high diversity of these sequences ensures that each RNA molecule is tagged with a distinct identifier, allowing for accurate counting and reducing biases introduced by PCR amplification.

## Raw read counts

Raw read counts in the context of RNA sequencing (RNA-seq) refer to the initial number of reads (short sequences of nucleotides) that are generated by sequencing technology and mapped back to a reference genome or transcriptome. Here's an overview:

1. **RNA Sequencing Process**:
   - RNA molecules are extracted from cells or tissues.
   - These RNA molecules are converted into complementary DNA (cDNA) through reverse transcription.
   - The cDNA is then sequenced, generating millions of short reads.

2. **Reads**:
   - Each read represents a fragment of the original RNA molecule.
   - These reads are typically 50-150 base pairs in length, depending on the sequencing technology used.

3. **Mapping Reads**:
   - The generated reads are aligned or mapped to a reference genome or transcriptome.
   - The process of mapping assigns each read to a specific gene or genomic location.

4. **Counting Reads**:
   - Raw read counts are the number of reads that map to each gene or transcript.
   - These counts provide a measure of the abundance of each RNA molecule in the sample.

5. **Purpose**:
   - Raw read counts serve as the starting point for downstream analysis in RNA-seq studies.
   - They are used to quantify gene expression levels, identify differentially expressed genes, and perform other types of genomic analyses.

However, raw read counts can be influenced by various _technical biases_, such as PCR amplification artifacts and differences in sequencing depth. To account for these factors, normalization techniques and the use of UMIs (Unique Molecular Identifiers) are often employed to obtain more accurate estimates of gene expression levels.

In summary, raw read counts are the initial counts of sequencing reads that map to genes or transcripts, providing a fundamental measure of RNA abundance before further processing and normalization.

### PCR Artifacts

PCR (Polymerase Chain Reaction) amplification artifacts can significantly affect raw read counts in RNA sequencing (RNA-seq) by introducing biases and distortions in the data. Here are the main ways PCR artifacts impact raw read counts:

1. **Over-Representation of Certain Sequences**:
   - During PCR amplification, some RNA fragments can be preferentially amplified over others due to sequence-specific biases or the efficiency of the primers used. This leads to an over-representation of these sequences in the final read counts.
   
2. **PCR Duplicates**:
   - Each original RNA molecule should ideally be represented by a unique read in the sequencing data. However, PCR can generate multiple copies (duplicates) of the same RNA molecule. These duplicates are indistinguishable from genuinely unique reads in raw read count data, inflating the apparent abundance of certain RNA molecules.

3. **Random Amplification Errors**:
   - PCR amplification can introduce random errors, such as nucleotide misincorporations, which can create reads that do not accurately reflect the original RNA sequence. These errors can complicate the mapping process and lead to incorrect read assignments.

4. **Amplification Efficiency Variability**:
   - The efficiency of PCR amplification can vary across different RNA molecules, leading to variable amplification rates. Some sequences might amplify more efficiently than others, causing discrepancies in the final read counts that do not accurately reflect the original RNA molecule abundance.

### Mitigating PCR Artifacts

1. **Unique Molecular Identifiers (UMIs)**:
   - As previously mentioned, UMIs can be used to tag each original RNA molecule before PCR amplification. By counting the number of unique UMIs instead of raw reads, researchers can more accurately estimate the true abundance of each RNA molecule and reduce the impact of PCR duplicates.

2. **Normalization Techniques**:
   - Applying normalization methods to adjust for sequencing depth and other technical variations helps to reduce the impact of PCR amplification biases on the final data.

3. **Duplicate Removal**:
   - Bioinformatics tools can identify and remove PCR duplicates by looking for reads that start and end at the same position in the genome, which are likely to be PCR artifacts.

In summary, PCR amplification artifacts can lead to over-representation, duplication, and errors in raw read counts, thus skewing the data. Employing techniques like UMIs, normalization, and duplicate removal can help mitigate these issues and produce more accurate measures of RNA abundance.

## Read depth calculation

Read depth, also known as sequencing depth or coverage, is calculated from sequencing results by determining the average number of times each nucleotide in the genome or transcriptome is sequenced. Here's how read depth is typically calculated:

1. **Obtain Sequencing Data**:
   - After sequencing, you have a collection of sequencing reads in a **FASTQ** file. These reads need to be processed and aligned to a reference genome or transcriptome.

2. **Quality Control and Trimming**:
   - Perform quality control (QC) on the raw reads using tools like FastQC to check for issues such as low-quality bases and adapter contamination.
   - Trim low-quality bases and adapter sequences using tools like Trimmomatic or Cutadapt.

3.  **Align Reads to Reference**:
   - Use an alignment tool (e.g., STAR, HISAT2 for RNA-seq; BWA, Bowtie2 for DNA-seq) to map sequencing reads to the reference genome or transcriptome.
   - The output of this alignment process is typically a **SAM or BAM** file, which contains information about where each read aligns on the reference.

4. **Count Aligned Reads**:
   - Count the number of reads that align to each position in the reference genome or transcriptome. This can be done using tools like `samtools depth`, `bedtools coverage`, or specialized RNA-seq quantification tools like HTSeq-count or featureCounts.
   
   Example command using `samtools depth`:
   ```bash
   samtools depth aligned_reads.bam > depth.txt
   ```
   The `depth.txt` file will contain the depth of coverage for each position in the genome.

5. **Calculate Average Read Depth**:
   - To calculate the average read depth, sum the depths of all positions and divide by the total number of positions covered.

   Example calculation:
   ```bash
   total_depth = sum(depths at all positions)
   number_of_positions = total number of positions covered
   average_read_depth = total_depth / number_of_positions
   ```

### Detailed Example

1. **Align Reads**:
   - Suppose you have 50 million reads from an RNA-seq experiment, and you align them to a reference genome using an aligner like HISAT2.
   - The alignment process results in a BAM file (`aligned_reads.bam`).

2. **Count Aligned Reads**:
   - Use `samtools depth` to count the reads at each position.
     ```bash
     samtools depth aligned_reads.bam > depth.txt
     ```

3. **Extract Depth Information**:
   - The `depth.txt` file will look something like this:
     ```
     chr1    1    30
     chr1    2    32
     chr1    3    35
     ...
     ```
     Each line represents a genomic position and the number of reads covering that position.

4. **Calculate Average Read Depth**:
   - Sum the coverage values and divide by the number of positions covered.

   ``` python
   depths = []
   with open('depth.txt') as file:
       for line in file:
           parts = line.split()
           depth = int(parts[2])
           depths.append(depth)

   total_depth = sum(depths)
   number_of_positions = len(depths)
   average_read_depth = total_depth / number_of_positions

   print(f"Average Read Depth: {average_read_depth}")
   ```

### Read Depth in RNA-Seq

In RNA-seq, read depth is often summarized at the level of genes or exons rather than individual nucleotides. Here's how you calculate it:

1. **Feature Quantification**:
   - Tools like HTSeq-count or featureCounts assign reads to genomic features (e.g., genes, exons) and provide counts for each feature.

2. **Summarize Read Depth**:
   - Calculate read depth per feature by dividing the total number of reads mapped to that feature by the length of the feature (e.g., length of the gene or exon).

### Example of RNA-Seq Feature Quantification

1. **Using HTSeq-count**:
   - Align reads to the reference genome.
   - Use HTSeq-count to quantify reads per gene.

     ```bash
     htseq-count -f bam -s no aligned_reads.bam genes.gtf > gene_counts.txt
     ```

2. **Calculate Depth per Gene**:
   - The output `gene_counts.txt` contains read counts for each gene.
   - Divide the read count by the gene length to get the depth for each gene.

### Summary

- **Align Reads**: Map sequencing reads to the reference genome.
- **Count Aligned Reads**: Count the number of reads at each position using tools like `samtools depth`.
- **Calculate Average Read Depth**: Sum the depths at all positions and divide by the number of positions covered.
- **Feature Quantification (RNA-Seq)**: Use tools like HTSeq-count to quantify reads per gene or feature and calculate depth per feature.

By following these steps, you can accurately calculate the read depth from sequencing results, providing insights into the coverage and quality of your sequencing data.
