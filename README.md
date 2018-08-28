# A continually expanding collection of scRNA-seq tools

Issues with suggestions and pull requests are welcome!

# Table of content

* [Preprocessing pipelines](#preprocessing-pipelines)
* [Normalization](#normalization)
* [Batch effect](#batch-effect)
* [Dimensionality reduction](#dimensionality-reduction)
* [Clustering and visualization](#clustering-and-visualization)
  * [Networks](#networks)
* [Differential expression](#differential-expression)
* [10X Genomics](#10x-genomics)
  * [QC](#10x-qc)
* [Data](#data)
  * [10X genomics brain data](#10x-data)

## Preprocessing pipelines

- `SEQC` - Single-Cell Sequencing Quality Control and Processing Software, a general purpose method to build a count matrix from single cell sequencing reads, able to process data from inDrop, drop-seq, 10X, and Mars-Seq2 technologies. https://github.com/ambrosejcarr/seqc
    - Azizi, Elham, Ambrose J. Carr, George Plitas, Andrew E. Cornish, Catherine Konopacki, Sandhya Prabhakaran, Juozas Nainys, et al. “Single-Cell Map of Diverse Immune Phenotypes in the Breast Tumor Microenvironment.” Cell, June 2018. https://doi.org/10.1016/j.cell.2018.05.060.

- `Seurat` - an R package designed for QC, analysis, and exploration of single cell RNA-seq data. Single-cell RNA-seq for spatial cellular localization, using in situ RNA patterns as a reference. Impute landmark genes, relate them to the reference map. http://satijalab.org/seurat/, https://davetang.org/muse/2017/08/01/getting-started-seurat/
    - Satija, Rahul, Jeffrey A. Farrell, David Gennert, Alexander F. Schier, and Aviv Regev. “Spatial Reconstruction of Single-Cell Gene Expression Data.” Nature Biotechnology 33, no. 5 (May 2015): 495–502. https://doi.org/10.1038/nbt.3192.
 



## Normalization

- `SCnorm` - normalization for single-cell data. Quantile regression to estimate the dependence of transcript expression on sequencing depth for every gene. Genes with similar dependence are then grouped, and a second quantile regression is used to estimate scale factors within each group. Within-group adjustment for sequencing depth is then performed using the estimated scale factors to provide normalized estimates of expression. Good statistical methods description. https://www.biostat.wisc.edu/~kendzior/SCNORM/
    - Bacher, Rhonda, Li-Fang Chu, Ning Leng, Audrey P Gasch, James A Thomson, Ron M Stewart, Michael Newton, and Christina Kendziorski. “SCnorm: Robust Normalization of Single-Cell RNA-Seq Data.” Nature Methods 14, no. 6 (April 17, 2017): 584–86. https://doi.org/10.1038/nmeth.4263.


## Batch effect

- `MNN` - mutual nearest neighbors method for single-cell batch correction. Assumptions: MNN exist between batches, batch is orthogonal to the biology. Cosine normalization, Euclidean distance, a pair-specific barch-correction vector as a vector difference between the expression profiles of the paired cells using selected genes of interest and hypervariable genes. Supplementary note 5 - algorithm. mnnCorrect function in the scran package https://bioconductor.org/packages/release/bioc/html/scran.html. Code for paper https://github.com/MarioniLab/MNN2017/
    - Haghverdi, Laleh, Aaron T L Lun, Michael D Morgan, and John C Marioni. “Batch Effects in Single-Cell RNA-Sequencing Data Are Corrected by Matching Mutual Nearest Neighbors.” Nature Biotechnology, April 2, 2018. https://doi.org/10.1038/nbt.4091.

## Dimensionality reduction

- `ZIFA` - Zero-inflated dimensionality reduction algorithm for single-cell data. Single-cell dimensionality reduction. Model dropout rate as double exponential, give less weights to these counts. EM algorithm that incorporates imputation step for the expected gene expression level of drop-outs. https://github.com/epierson9/ZIFA
    - Pierson, Emma, and Christopher Yau. “ZIFA: Dimensionality Reduction for Zero-Inflated Single-Cell Gene Expression Analysis.” Genome Biology 16 (November 2, 2015): 241. https://doi.org/10.1186/s13059-015-0805-z.

- `ZINB-WAVE` - Zero-inflated negative binomial model for normalization, batch removal, and dimensionality reduction. Extends the RUV model with more careful definition of "unwanted" variation as it may be biological. Good statistical derivations in Methods. Refs to real and simulated scRNA-seq datasets. https://bioconductor.org/packages/release/bioc/html/zinbwave.html
    - Risso, Davide, Fanny Perraudeau, Svetlana Gribkova, Sandrine Dudoit, and Jean-Philippe Vert. “ZINB-WaVE: A General and Flexible Method for Signal Extraction from Single-Cell RNA-Seq Data.” BioRxiv, January 1, 2017. https://doi.org/10.1101/125112.



## Clustering and visualization

- `Bisquit` - a Bayesian clustering and normalization method. https://github.com/sandhya212/BISCUIT_SingleCell_IMM_ICML_2016
    - Azizi, Elham, Ambrose J. Carr, George Plitas, Andrew E. Cornish, Catherine Konopacki, Sandhya Prabhakaran, Juozas Nainys, et al. “Single-Cell Map of Diverse Immune Phenotypes in the Breast Tumor Microenvironment.” Cell, June 2018. https://doi.org/10.1016/j.cell.2018.05.060.

- `destiny` - R package for diffusion maps-based visualization of single-cell data. https://bioconductor.org/packages/release/bioc/html/destiny.html
    - Haghverdi, Laleh, Florian Buettner, and Fabian J. Theis. “Diffusion Maps for High-Dimensional Single-Cell Analysis of Differentiation Data.” Bioinformatics 31, no. 18 (September 15, 2015): 2989–98. https://doi.org/10.1093/bioinformatics/btv325. - Introduction of other methods, Table 1 compares them. Methods details. Performance is similar to PCA and tSNE. 

- `PhenoGraph` - discovers subpopulations in scRNA-seq data. High-dimensional space is modeled as a nearest-neighbor graph, then the Louvain community detection algorithm. No assumptions about the size, number, or form of subpopulations. https://github.com/jacoblevine/PhenoGraph
    - Levine, Jacob H., Erin F. Simonds, Sean C. Bendall, Kara L. Davis, El-ad D. Amir, Michelle D. Tadmor, Oren Litvin, et al. “Data-Driven Phenotypic Dissection of AML Reveals Progenitor-like Cells That Correlate with Prognosis.” Cell 162, no. 1 (July 2015): 184–97. https://doi.org/10.1016/j.cell.2015.05.047.

- SIMLR - scRNA-seq dimensionality reduction, clustering, and visualization based on multiple kernel-learned distance metric. Comparison with PCA, t-SNE, ZIFA. Seven datasets. R and Matlab implementation. https://github.com/BatzoglouLabSU/SIMLR
    - Wang, Bo, Junjie Zhu, Emma Pierson, Daniele Ramazzotti, and Serafim Batzoglou. “Visualization and Analysis of Single-Cell RNA-Seq Data by Kernel-Based Similarity Learning.” Nature Methods 14, no. 4 (April 2017): 414–16. https://doi.org/10.1038/nmeth.4207.

- `viSNE` - the Barnes-Hut implementation of the t-SNE algorithm, improved and tailored for the analysis of single-cell data. Details of tSNE https://www.denovosoftware.com/site/manual/visne.htm, and the `Rtsne` R package https://cran.r-project.org/web/packages/Rtsne/index.html
    - Amir, El-ad David, Kara L Davis, Michelle D Tadmor, Erin F Simonds, Jacob H Levine, Sean C Bendall, Daniel K Shenfeld, Smita Krishnaswamy, Garry P Nolan, and Dana Pe’er. “ViSNE Enables Visualization of High Dimensional Single-Cell Data and Reveals Phenotypic Heterogeneity of Leukemia.” Nature Biotechnology 31, no. 6 (June 2013): 545–52. https://doi.org/10.1038/nbt.2594.

### Networks

- `SCENIC` - single-cell network reconstruction and cell-state identification. Three modules: 1) GENIE3 - connect co-expressed genes and TFs using random forest regression; 2) RcisTarget - Refine them using cis-motif enrichment; 3) AUCell - assign activity scores for each network in each cell type. https://gbiomed.kuleuven.be/english/research/50000622/lcb/tools/scenic, https://github.com/aertslab/SCENIC, https://github.com/aertslab/GENIE3, https://github.com/aertslab/AUCell
    - Aibar, Sara, Carmen Bravo González-Blas, Thomas Moerman, Vân Anh Huynh-Thu, Hana Imrichova, Gert Hulselmans, Florian Rambow, et al. “SCENIC: Single-Cell Regulatory Network Inference and Clustering.” Nature Methods 14, no. 11 (November 2017): 1083–86. https://doi.org/10.1038/nmeth.4463.


## Differential expression

- Soneson, Charlotte, and Mark D Robinson. “Bias, Robustness and Scalability in Single-Cell Differential Expression Analysis.” Nature Methods, February 26, 2018. https://doi.org/10.1038/nmeth.4612. - Differential analysis of scRNA-seq data, 36 methods. Prefiltering of low expressed genes is important. edgeRQLFDetRate performs best. The conquer database, scRNA-seq datasets as RDS objects - http://imlspenticton.uzh.ch:3838/conquer/


- `MAST` - scRNA-seq DEG analysis. CDR - the fraction of genes that are detectably expressed in each cell - added to the hurdle model that explicitly parameterizes distributions of expressed and non-expressed genes. Generalized linear model, log2(TPM+1), Gaussian. Regression coeffs are estimated using Bayesian approach. Variance shrinkage, gamma distribution. https://github.com/RGLab/MAST
    - Finak, Greg, Andrew McDavid, Masanao Yajima, Jingyuan Deng, Vivian Gersuk, Alex K. Shalek, Chloe K. Slichter, et al. “MAST: A Flexible Statistical Framework for Assessing Transcriptional Changes and Characterizing Heterogeneity in Single-Cell RNA Sequencing Data.” Genome Biology 16 (December 10, 2015): 278. https://doi.org/10.1186/s13059-015-0844-5.



-  `SCDE`. Stochasticity of gene expression, high drop-out rate. A mixture model of two processes - detected expression and drop-out failure modeled as low-magnitude Poisson. Drop-out rate depends on the expected expression and can be approximated by logistic regression. https://hms-dbmi.github.io/scde/index.html
    - Kharchenko, Peter V., Lev Silberstein, and David T. Scadden. “Bayesian Approach to Single-Cell Differential Expression Analysis.” Nature Methods 11, no. 7 (July 2014): 740–42. https://doi.org/10.1038/nmeth.2967.




## 10X Genomics

- Zheng, Grace X. Y., Jessica M. Terry, Phillip Belgrader, Paul Ryvkin, Zachary W. Bent, Ryan Wilson, Solongo B. Ziraldo, et al. “Massively Parallel Digital Transcriptional Profiling of Single Cells.” Nature Communications 8 (January 16, 2017): 14049. https://doi.org/10.1038/ncomms14049. - 10X technology. Details of each wet-lab step, sequencing, and basic computational analysis. scRNA- Seq dataset of 3000 peripheral blood mononuclear cells (PBMCs) from the 10X Genomics platform. https://support.10xgenomics.com/single-cell-gene-expression/datasets

- Cell Ranger, Loupe Cell Browser software download, https://support.10xgenomics.com/single-cell-gene-expression/software/downloads/latest

- Cell Ranger R kit, https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/rkit

### 10X QC

- `bxcheck` - Toolset for QC and processing 10x genomics data. https://github.com/pd3/bxcheck

## Data

### 10X data

- The 1 million neuron data set from the 10X Genomics website (https://support.10xgenomics.com/single-cell-gene-expression/datasets). R packages for its analyses: 
    - `TENxGenomics` - https://github.com/mtmorgan/TENxGenomics
    - `TENxBrainAnalysis` - https://github.com/Bioconductor/TENxBrainAnalysis

- Multiple datasets, https://support.10xgenomics.com/single-cell-gene-expression/datasets



