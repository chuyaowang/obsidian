# Proximity Guided Gene Embedding

chatgpt answer

These are [Graph Embedding](Graph%20Embedding.md) methods used for embedding genes while preserving the local neighborhood structure of genes in the [Gene Regulatory Network](Gene%20Regulatory%20Network.md). Some examples are:

1. **Node2Vec**: 2016, 12105 cited
   - **Description**: [Node2Vec](Graph%20Neural%20Network.md#Node2Vec) is a popular method that learns continuous feature representations for nodes in a network by optimizing a neighborhood-preserving objective. It uses a biased random walk strategy to generate sequences of nodes, which are then used to train a skip-gram model.
   - **Application to Genes**: When applied to gene networks, Node2Vec captures the local and global structure by embedding genes such that genes appearing in similar contexts (i.e., sharing many common neighbors) are placed close to each other in the embedding space.

2. **DeepWalk**: 2014, 11142 cited
   - **Description**: DeepWalk performs random walks on the graph to generate a set of node sequences and then applies the skip-gram model from natural language processing to learn node embeddings.
   - **Application to Genes**: For gene networks, DeepWalk captures the relationships and proximities between genes based on the _co-occurrences_ within the generated random walks, thus preserving the local neighborhood structure in the embedding space.

3. **LINE (Large-scale Information Network Embedding)**: 2015, 6256 cited
   - **Description**: LINE aims to preserve both the first-order proximity (direct connections between nodes) and second-order proximity (similarity between nodes' neighbors). It does this by separately modeling these proximities and then combining the embeddings.
   - **Application to Genes**: In gene networks, LINE can embed genes such that directly connected genes (first-order proximity) and genes with similar neighbor structures (second-order proximity) are placed close to each other.

4. **HOPE (High-Order Proximity preserved Embedding)**: 2018, 152 cited
   - **Description**: HOPE is designed to capture high-order proximities in large-scale networks. It uses matrix factorization techniques to preserve higher-order proximities, such as Katz index, Rooted PageRank, etc.
   - **Application to Genes**: HOPE can be used to embed genes in a way that reflects both direct and indirect relationships, capturing the complex interactions in gene networks.

5. **GraRep (Graph Representations)**: 2015, 1936 cited
   - **Description**: GraRep captures k-step relationships by constructing multiple k-step transition matrices and factorizing them to obtain embeddings. It captures both local and global structures.
   - **Application to Genes**: In gene networks, GraRep can capture the multi-step relationships between genes, embedding genes with similar multi-step neighborhood structures close to each other.

These proximity-based gene embedding methods focus on preserving the local and sometimes global structure of the gene interaction network. They are particularly useful for tasks where the local neighborhood relationships are important, such as clustering genes with similar functions or predicting gene interactions. 

However, as mentioned earlier, they may not be optimal for [aligning genes from separate networks](Gene2role%20a%20role-based%20gene%20embedding%20method%20for%20comparative%20analysis%20of%20signed%20gene%20regulatory%20networks.md) for comparative analysis without additional steps to incorporate [cross-network correspondences](struc2vec%20Learning%20Node%20Representations%20from%20Structural%20Identity.md).