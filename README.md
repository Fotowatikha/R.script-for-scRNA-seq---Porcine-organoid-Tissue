# Single-Cell Pre-Processing Script

Now considering that the emergence of scRNA-seq techniques provides the framework to study gene expression variability in organoids or tissue of interest, the pre-processing of high dimensional RNA-seq data also becomes an important topic. To this day, droplet-based technologies remain the technique of choice when it comes to capturing and sequencing a large number of individual cells. This method essentially barcodes single cells and tags each transcript with a unique molecular identifier (UMI) within individual droplets, which can significantly increase the throughput up to 10,000 cells per analysis. However, this technique is not free of noise, and one must carefully pre-process the data before any unbiased downstream analysis can be caried out. 

**Here, I will provide you with all the necessary information on how to use my single-cell pre-processing script, either on your local system or on the HPC. I will also provide you with the information you need for a Snakemake implementation.**

## About

By consider the gene count matrices as the starting point after mapping reads to the reference, the major steps in this pre-processing is to: (1) Provide the user with quality control (QC) plots to gain insight on the overall quality of the cells prior to any extensive filtering; (2) Correcting the data from cell-free ambient RNA; (3) Extensive filtering to remove droplets that are unlikely to represent intact individual cells; (4) Removal of droplets that violate the assumption for containing one cell; (5) Provide the user with QC plots to gain insight on the quality of the data post-filtering.

**More detail each step and what to expect from the output is provided below. For each sept, example pictures are provided and how you should read them.**

## How run it on the HPC (no Conda) or on your local system

Now provided that I was unsuccessful in implementing the pre-processing script with Cellranger in a Snakefile that is compatible with the Conda environment (more on that later), i will explain to you how to run it outside a Snakefile.
