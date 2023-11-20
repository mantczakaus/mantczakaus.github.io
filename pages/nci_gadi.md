---
title:
contributors: 
description: 
affiliations: 
---


### Directly on the HPC
#### Download databases
Tools in the ONTvisc pipeline compare the reads/clusters/contigs (depending on the mode) to a database or a reference. The explanation of which databases are required to be provided depending on the selected mode and tips on how to install them can be found in the pipeline's wiki page in the <a href="https://github.com/maelyg/ontvisc/wiki/Installation#installing-the-required-indexes-and-references"> Installing the required indexes and references </a> section. Below commands that will download the respective databases on Gadi. Change paths to folders / links / versions if necessary. Make sure you create a folder where you will store all the databases first and update the scripts when necessary.
##### NT - BlastDB
The following script will:
1) Create a folder ```blastDB``` in the folder ```/scratch/go97/ontvisc/databases```
2) Create a script ```download_blastdb.pbs``` that downloads a perl script update_blastdb.pl which will download and decompress all the necessary components of the NT database
3) Submit the ```download_blastdb.pbs``` script to PBS
Create a folder where you'll want to store the BlastDB, e.g.
```bash
blastdb_fold=/scratch/go97/ontvisc/databases/blastDB
mkdir -p $blastdb_fold
cd $blastdb_fold

cat <<EOF > download_blastdb.pbs
#!/bin/bash -l
#PBS -N d_blastdb
#PBS -l mem=60gb
#PBS -l walltime=08:00:00
#PBS -q copyq

curl -sO ftp://ftp.ncbi.nlm.nih.gov/blast/temp/update_blastdb.pl
chmod +x update_blastdb.pl
perl update_blastdb.pl --decompress nt
perl update_blastdb.pl taxdb
tar -xzf taxdb.tar.gz
EOF

qsub download_blastdb.pbs
```
##### Kraken
##### Kaiju
##### VirDB
#### Download the pipeline and singularity images (if you are planning to use a queue that does not have network connection)

#### Run Tower Agent

### In GitHub


### In Nextflow Tower
#### Create a Personal Access Token
#### Add Credentials for Tower Agent
#### Add Credentials for GitHub
#### Add a Compute Environment
#### Add a pipeline



### Useful links
### Submit scripts to PBS

