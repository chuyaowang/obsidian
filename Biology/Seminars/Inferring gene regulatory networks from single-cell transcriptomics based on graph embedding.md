# IGEGRNS

[Paper](https://academic.oup.com/bioinformatics/article/40/5/btae291/7684950?login=false)
[IGEGRNS](IGEGRNS.pdf)
[Github](https://github.com/DHUDBlab/IGEGRNS)
[BEELINE](https://pubmed.ncbi.nlm.nih.gov/31907445/): a GRN inference algorithm evaluation framework, highly cited
#paper 

Supervised GRN inference model. Low performance in real data. Poor documentation. Not really useful. Taking notes for study purpose.

Requires reference network to train the model before making predictions.
## Introduction

[Gene Regulatory Network](Gene%20Regulatory%20Network.md) inference is the process of predicting [Transcription Factor](Transcription%20Factor.md) - Gene interactions from gene expression data. There are [Unsupervised](0.%20Understanding%20Deep%20Learning.md#Unsupervised%20Learning) and [Supervised Learning](0.%20Understanding%20Deep%20Learning.md#Supervised%20Learning) methods. 

In general, these methods composed of two steps:
1. Converting the gene expression data to a suitable format
2. Use deep learning methods to predict the regulatory relationship

IGEGRNS composed of three steps:
1. Use [GraphSAGE](Graph%20Neural%20Network.md#GraphSAGE) to generate node embeddings
2. Use top-k pooling to select nodes most important for the graph. Then combine the k nodes and two genes to be predicted into a matrix.
3. Train a 3 layer CNN network for [link prediction](Graph%20Embedding.md#^1f1a81). The links represent interactions between TF and gene. The matrix in step 2 is fed to the network, and whether there is link in the reference network is used to train the model.

**Time series** [scRNA-seq](scRNA-seq.md) data were used to evaluate the method.

## Methods

### The model

GraphSAGE requires previous link knowledge and the gene expression matrix to compute node embeddings. Authors evaluated multiple model parameters:
- hop (search depth) = 1
- vector dimension = 256
- Mean aggregator function; performs better than LSTM and Max

Then the input matrix is generated.

The stacked CNN layer is used to predict link existence.
- number of layers = 3 is the best
- each layer consists of a BatchNorm layer, a CNN convolution layer, and a maximum pooling layer

The CNNs serve as further feature extraction to further learn the high-level feature representation, increase the nonlinear capability of the network, and better capture the complex relationships hidden in the data.

### Evaluation

Using 6 time-series scRNA datasets, 5 fold cross validation was performed to test the method against other unsupervised and supervised methods. AUROC and AUPRC scores were computed for each model.

Only analyzed highly variable TFs and top 500 and 1000 most differential genes. Filtering only highly variable genes is also used in [bioIB](Identifying%20maximally%20informative%20signal-aware%20representations%20of%20single-cell%20data%20using%20the%20Information%20Bottleneck.md) to reduce compute time.
## Results

### Evaluation

Naturally, the supervised methods outperformed the unsupervised methods.

### Real data

Used two reference networks and two real time-series datasets to evaluate their method. The reference networks were used to train the model and evaluate the result.

AUROC (around 0.7) and AUPRC (around 0.45) considerably lower than in evaluation datasets. Could be an issue with the data?

Interestingly they did not measure how many links that do not exist in the reference network were predicted by the model.

## Data sources

Riken TFDB for mouse GRN
animalTFDB for human GRN

Gene expression raw data are available in NCBI GEO database under the following accession numbers: 
human embryonic stem cells (hESC): GSE75748
human mature hepatocytes (hHEP): GSE81252
mouse embryonic stem cells(mESC): GSE98664
mouse blood stem/progenitor cell (mHSC): GSE81682.

