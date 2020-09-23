# Single-cell analyses for fate-seq
*presented in the article introducing fate-seq [(Meyer, Paquet et al., Cell Systems 2020](https://www.cell.com/cell-systems/fulltext/S2405-4712(20)30330-6)*

**Note 1**: Data files can be downloaded from Mendeley [here](https://data.mendeley.com/datasets/m289yp5skd/draft?a=65157631-161f-40a6-a718-23b0f9e6fa58).
Data should remain private until this work is accepted for publication, please do not share without consent from the authors.

**Note 2**: This code was developed under R 3.6.1. It was not tested on more recent versions of R.

Our results are based on the analysis of two types of data:
* The fate-seq dataset, which comprises a small subset of HeLa cells treated with TRAIL, carefully analyzed using a combination of live-cell microscopy, laser capture microscopy, and profiled using our single cell RNAseq protocol.
* A shallow single-cell RNAseq profiling of HeLa cell after brief treatment with TRAIL, using the 10x Genomics technology.
Below is a short description of the bioinformatics methods used to analyze these data; the R code used to generate the figures for the paper is provided in this repository.

### analysis_10x_adjusting_for_cellcycle.Rmd
R code for the analysis of the 10x data. Analyses were performed using standard Seurat V3 pipeline, including hashtag processing and demultiplexing, QC, correction for cell cycle, data integration, dimension reduction, clustering and visualization. We used our own set of gene for cell cycle assessment provided here in the file Barbry-CellCycle_GeneSets.txt (Revinski et al, 2018).


### Bulk_Analysis_ForPaper.Rmd
PseudoBulk analysis of the 10x data: Two pseudo-bulk samples were constructed from each single cell sample by randomly selecting 700 cells (without replacement) among all cells passing quality filter, then, we calculated the UMI count value for each gene by adding the UMIs counts corresponding to this gene from these 700 cells. Statistical analysis of bulk samples was performed using the R package _**edgeR**_

### Rcode_Roux_ms_2020_fate-seq_file_1.Rmd
This file contains the R code for the statistical analysis of the fate-seq dataset, performed using Bioconductor packages _**scran**_ and _**edgeR**_. Heatmap were generated using pheatmap. Cell cycle assessment was performed using the algorithm described before (Macosko et al, 2015), based on our curated gene sets, provided here Barbry-CellCycle_GeneSets.txt (Revinski et al, 2018)

### References

Macosko EZ, Basu A, Satija R, Nemesh J, Shekhar K, Goldman M, Tirosh I, Bialas AR, Kamitaki N, Martersteck EM, Trombetta JJ, Weitz DA, Sanes JR, Shalek AK, Regev A & McCarroll SA (2015) Highly Parallel Genome-wide Expression Profiling of Individual Cells Using Nanoliter Droplets. Cell 161: 1202–1214

Revinski DR, Zaragosi L-E, Boutin C, Ruiz García S, Deprez M, Thomé V, Rosnet O, Gay A-S, Mercey O, Paquet A, Pons N, Ponzio G, Marcet B, Kodjabachian L & Barbry P (2018) CDC20B is required for deuterosome-mediated centriole production in multiciliated cells. Nat Commun 9: 4668

