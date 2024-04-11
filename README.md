R.script-for-scRNA-seq---Porcine-organoid-Tissue

This repository contains all the R scripts (RMD format) that were created and used for the analysis of single-cell RNA-sequencing data throughout this MSc thesis.
By consider the gene count matrices as the starting point after mapping reads in CellRanger, script for quality control and pre-processing is provided so that it can run on your local system. (The full pipeline will published in a separate public repository).
Scripts for the analysis of the data (ileum, organoid) are contained within chunks, with each chunk carrying out a different task (e.g. cell-cell communication network, clustering, GO, trajectory analysis and more).
Note that the scripts are heavily personalized (for my local system) and specialized towards the analysis of the data used for this thesis. While most chunks and lines are documented, I do not recommend using them to reproduce the results in a different animal/tissue/organoid.
General purpose scripts to perform the same analysis in different animal/tissue/organoid will be published on a later date (in the same repository). The chunks will be replaced with separate R scripts for every type of analysis.
For some analysis (WGCNA and CellChat) previous versions of Seurat has been used. These codes will be updated to be compatible with the latest version on a later date. All the other codes have been rewritten to be compatible with Seurat_v5, however you will find some lines that were used for the previous version. These lines have been greyed-out, so you can ignore them.
(THIS README FILE WILL CHANGE ONCE ALL THE GENERAL-PURPOSE SCRIPTS ARE UPLOADED. EVERYTHING ELSE AS IS NOW)

If you are the next student doing a thesis at ABG on single-cell data, feel free to contact me (https://twitter.com/H_Fotowaikha) if you need assistance with the existing code that was used for this analysis.

I do recommend to stay away from Seurat if you want to save yourself some sleepless nights during your thesis. The developers love to implement meaningless updates that will move your count matrices in layers. You can of course parse things manually, but that will take you a lot of time. I recommend you to use Scanpy from the start, unless some package you need is not available in Python.
