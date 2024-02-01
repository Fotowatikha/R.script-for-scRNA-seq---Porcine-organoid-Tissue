# Single-Cell Pre-Processing Script

Now considering that the emergence of scRNA-seq techniques provides the framework to study gene expression variability in organoids or tissue of interest, the pre-processing of high dimensional RNA-seq data also becomes an important topic. To this day, droplet-based technologies remain the technique of choice when it comes to capturing and sequencing a large number of individual cells. This method essentially barcodes single cells and tags each transcript with a unique molecular identifier (UMI) within individual droplets, which can significantly increase the throughput up to 10,000 cells per analysis. However, this technique is not free of noise, and one must carefully pre-process the data before any unbiased downstream analysis can be caried out. 

**Here, I will provide you with all the necessary information on how to use my single-cell pre-processing script, either on your local system or on the HPC. I will also provide you with the information you need for a Snakemake implementation.**

## About

By consider the gene count matrices as the starting point after mapping reads to the reference, the major steps in this pre-processing is to: (1) Provide the user with quality control (QC) plots to gain insight on the overall quality of the cells prior to any extensive filtering; (2) Correcting the data from cell-free ambient RNA; (3) Extensive filtering to remove droplets that are unlikely to represent intact individual cells; (4) Removal of droplets that violate the assumption for containing one cell; (5) Provide the user with QC plots to gain insight on the quality of the data post-filtering.


**More detail each step and what to expect from the output is provided below. For each sept, example pictures are provided and how you should read them.**

## How run it on the HPC (no Conda) or on your local system

Now provided that I was unsuccessful in implementing the pre-processing script with Cellranger in a Snakefile that is compatible with the Conda environment (more on that later), i will explain to you how to run it outside a Snakefile.

On your local system you can run the pre-processing.Rmd script on **Rstudio** or render it as an Rscript on your terminal using by running: 

```sh
Rscript -e "rmarkdown::render('pre-processing.Rmd’)
```

The most important part here is that you will be able to specify the correct paths to the output folder provided by Cellranger counts. For the sake of clarity (also for Snakemake), at the start of the code, I have made separate chuck where all the user parameters can be adjusted. The advantages of this are that you no longer have to dig into code to enter the correct parameters. Likewise, you don’t have to dig into the code to setup the parameters in your `config.yaml` for Snakemake. I will explain the parameters in-depth later on, but it is not necessary to insert any parameters as I have already implemented an automated filtering that has proven to works very well with single-cell and single-nuclei datasets from porcine ileum, colon and organoids.

The two paths that you need to specify are the parent_directory and the sample_path. 

An example of a path looks like this:
`~/user/scRNA-intestine/sample1/outs`

When you run Cellranger counts, you have to specify the `--id`, such as `--id=sample1`. When finished running, Cellranger will put all the output files in that specific folder called `sample1`. 
So in this case the directories will look as follows: `parent_directory = "~/user/scRNA-intestine"` and the `sample_path = c("sample1")`. You type it down exactly as given in this example, so don’t put additional `/` at the start or the end. That’s it! Now you can run it on your local system after you install all the packages as specified in the first chunk of the code. So in case you have two samples, or three within the `parent_directory`, the only thing you have to do is to change is the sample_path to `sample_path = c("sample1", "sample2", "sample3)`. Boom! now you can pre-process multiple samples at the same time. To make sure your graphs in the output are labaled correctly, make sure to put the name of your experiments in the parameter called `sample_names`. Lke this `sample_names = c("brain", "eyes", "intestine")`. Now all your graphs will have the correct headers in the output.

But there is a catch, by running multiple samples, you are forced to use the same filtering parameters for all your samples. As of now, there is not option to pick different parameters for every sample. So it is recommended to use this pre-processing scripts for one sample at a time.
