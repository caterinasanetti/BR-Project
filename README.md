# BR-Project
This project was conducted as part of the Bioinformatics Resources course at the Università degli Studi di Trento.  This study involves a comprehensive bioinformatic analysis of RNA-seq data from UCEC tumor and normal samples.

## Authors

*   Rizzolo Maria Luce
*   Sanetti Caterina

## Overview
The study aims to identify differentially expressed genes (DEGs), perform functional enrichment analysis to understand affected biological pathways, investigate potential master transcriptional regulators through motif enrichment, and construct a protein-protein interaction (PPI) network to explore functional relationships among key genes. The analysis pipeline includes data loading, filtering, normalization, exploratory data analysis (hierarchical clustering, PCA), differential expression testing, gene set enrichment analysis (GSEA), motif enrichment in promoter regions, and network analysis with centrality measures and community detection.

## Data

The primary dataset consists of RNA-seq raw expression counts for Uterine Corpus Endometrial Carcinoma, retrieved from The Cancer Genome Atlas (TCGA). The dataset includes samples annotated as 'Case' (tumor) or 'Control' (normal). The initial data included ~63,000 gene identifiers which were subsequently filtered.

## Methods

The analysis workflow followed several key steps:

1.  **Data Loading and Filtering:** Raw counts were loaded and filtered to retain only protein-coding genes. Further filtering removed genes with low counts across samples to focus on robustly expressed transcripts.
2.  **Normalization:** Raw counts were normalized using the TMM (Trimmed Mean of M-values) method to account for library size differences, yielding Counts Per Million (CPM) values.
3.  **Exploratory Data Analysis:** Hierarchical clustering and Principal Component Analysis (PCA) were performed on the normalized data to assess sample relationships and identify global patterns related to the case/control status.
4.  **Differential Expression Analysis:** The edgeR package was used to perform differential expression testing between tumor and normal samples using the quasi-likelihood F-test. Genes were classified as up-regulated, down-regulated, or not differentially expressed based on predefined thresholds (FDR < 0.05, |log2 fold change| > 1.5, logCPM > 1).
5.  **Gene Set Enrichment Analysis (GSEA):** A ranked list of genes (by log2 fold change) was used with fgsea to identify enriched pathways in MSigDB collections (C4: computational gene sets, C6: oncogenic signatures).
6.  **Functional Enrichment Analysis (gProfiler & pathfindR):** Up- and down-regulated DEGs were analyzed using gProfiler2 (for GO:BP and KEGG terms) and pathfindR to identify significantly enriched biological processes and pathways, with a specific focus on key pathways like Cell Cycle.
7.  **Transcription Factor Motif Enrichment:** Promoter regions (500 bp upstream) of filtered genes from enriched MSigDB pathways were analyzed for enriched transcription factor binding motifs using PWMEnrich and MotifDb. Potential master regulators were identified based on consistent enrichment. Predicted binding sites for a selected candidate TF were explored using pattern matching.
8.  **Protein-Protein Interaction Network Analysis:** The STRING database was used to construct a network of interactions among the top up- and down-regulated DEGs. Network properties (degree distribution, centrality measures) were analyzed, the Largest Connected Component (LCC) was isolated and visualized, and community detection was performed to identify functional modules.

## Key Findings

*   Clear separation of Case and Control samples observed through clustering and PCA after normalization.
*   Identification of significant numbers of both up- and down-regulated genes in UCEC tumors.
*   GSEA highlighted key oncogenic pathways (e.g., AKT/MTOR signaling) and transcriptional signatures (e.g., HOXA9, Epithelial Senescence) as enriched.
*   Functional enrichment analysis of DEGs pointed to processes like mitotic cell cycle and steroid biosynthesis (up) and system development/signalind (down).
*   Cell Cycle (hsa04110) was strongly enriched among up-regulated genes, with key components (cyclins, MCMs) showing increased expression.
*   Motif enrichment analysis identified **NNT** as a top candidate for a master regulator, with predicted high-confidence binding sites in the promoters of **DRAP1** and **EZH2**.
*   Network analysis revealed a highly connected PPI network with **TNF**, **GAPDH**, and **ALB** identified as prominent hubs.
*   Community detection in the network revealed modules associated with key biological processes in cancer, including metabolism, senescence, and epithelial morphogenesis.

## Conclusions

The analysis successfully identified transcriptional signatures and potential regulatory mechanisms involved in UCEC. The clear distinction between tumor and normal samples allowed for robust identification of DEGs. Enrichment analyses highlighted dysregulated proliferation (via cell cycle activation) and altered developmental/signaling processes. The finding of NNT as a potential key transcription factor targeting genes like DRAP1 and EZH2 suggests a novel regulatory axis warrants further investigation. Network analysis provided insights into the complex interactions among DEGs and identified central players and functional modules. Future work could integrate other omics data to build a more complete picture of UCEC progression.

