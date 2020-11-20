# SZS Pipeline

This repository contains code to perform the analyses in the paper ["The SZS is a robust and efficient method to identify regulated splicing events in droplet-based RNA Sequencing" (Olivieri, Dehghannasiri, and Salzman 2020)](https://www.biorxiv.org/content/10.1101/2020.11.10.377572v1.abstract). 

This pipeline takes the output from [SICILIAN](https://github.com/salzmanlab/SICILIAN) and returns the SZS for each gene and cell, as well as analyses of differential alternative splicing.

![Pipeline](pipeline.png)


## Installation and setup

Clone this repository:
`git clone https://github.com/juliaolivieri/SZS_pipeline`

`cd SZS_pipeline/`

Ensure that conda is working on your system. If you are working on sherlock on the horence partition, you can try adding export PATH="/share/PI/horence/applications/anaconda3/bin/:$PATH"` to your .bashrc.

Then set up the conda environment from the environment.yml file:

`conda env create --name szs_env --file=environment.yml`

and activate it:

` source activate szs_env`

If this activation step doesn't work, try running `conda env list` and looking for the path that ends with `szs_env`. Then run `source activate <full path>`, for example `source activate /share/PI/horence/applications/anaconda3/envs/szs_env`.

You will need to place the following files in the "data" directory:
* `HLCA4_P2_10x_with_postprocessing_lung.pq`
* `HLCA4_P3_10x_with_postprocessing_lung.pq`

And the following files in the util_files directory:
* `GRCh38_latest_genomic.gtf`
* `ucscGenePfam.txt`

If you are working on Sherlock with access to the horence partition, you can run 

`cp /scratch/PI/horence/JuliaO/single_cell/SZS_pipeline/data/* data/`

and

`cp /scratch/PI/horence/JuliaO/single_cell/SZS_pipeline/util_files/* util_files/`

to get these files.

## Running the pipeline

Then run `snakemake -p` in the main directory (I run `snakemake -p --profile slurm` to run on sherlock). You can run `snakemake -np` first to see what jobs will be run.

To set up snakemake to run on slurm, you can follow the directions here: [https://github.com/Snakemake-Profiles/slurm](https://github.com/Snakemake-Profiles/slurm). If you are working on sherlock using the horence partition, you can try copying the folder `/scratch/PI/horence/JuliaO/snakemake` to `~/.config` by running `cp -r /scratch/PI/horence/JuliaO/snakemake ~/.config/` instead.

## References
Olivieri, Dehghannasiri, and Salzman. "The SZS is an efficient statistical method to identify regulated splicing events in droplet-based RNA sequencing." bioRxiv. (2020) [https://www.biorxiv.org/content/10.1101/2020.11.10.377572v1.abstract](https://www.biorxiv.org/content/10.1101/2020.11.10.377572v1.abstract).

Dehghannasiri, Olivieri, and Salzman. "Specific splice junction detection in single cells with SICILIAN," bioRxiv. (2020) [https://www.biorxiv.org/content/10.1101/2020.04.14.041905v1](https://www.biorxiv.org/content/10.1101/2020.04.14.041905v1).
