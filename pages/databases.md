---
title:Beyond test data and configuration
toc: false
---

Other usage examples can be found on the [Running the pipeline](https://github.com/eresearchqut/ONTViSc/tree/v1.3?tab=readme-ov-file#running-the-pipeline) section of the ONTViSc pipeline's guide. The examples include Nextflow commands with the required parameters for each mode, e.g. [Read classification analysis mode](https://github.com/eresearchqut/ONTViSc/tree/v1.3?tab=readme-ov-file#read-classification-analysis-mode).

## Check if required databases are provided on your HPC
Tools in the ONTViSc pipeline search/align the reads/clusters/contigs (depending on the mode) to a database or a reference. The explanation of which databases are required based on the selected mode, along with tips on how to install them, can be found in the section of the guide entitled <a href="https://github.com/eresearchqut/ontvisc/tree/v1.3?tab=readme-ov-file#installing-the-required-indexes-and-references"> Installing the required indexes and references </a>. Below are instructions for installing the necessary databases depending on the HPC.
#### Gadi
If access to Gadi was granted to you through the [ABLeS initiative](https://www.biocommons.org.au/ables), you have access to the [Australian BioCommons shared repository of tools and software](https://australianbiocommons.github.io/ables/if89/) under the project allocation if89 (you need to [join the if89 first](https://my.nci.org.au/mancini/project/if89)). Check the `/g/data/if89/data_library` folder for your needed databases. If they are not provided there, [contact the ABLeS team](https://australianbiocommons.github.io/ables/contact-us/) first to see if they can add them to the shared folder. If not, proceed with the installation yourself using the instructions below.
#### Setonix
Check if the databases you require are available in the folder `/scratch/references` (more details in the [Reference datasets](https://pawsey.atlassian.net/wiki/spaces/US/pages/51925876/Pawsey+Filesystems+and+their+Use#PawseyFilesystemsandtheirUse-Referencedatasets) section of the [Pawsey Filesystems and their Usage](https://pawsey.atlassian.net/wiki/x/dFMYAw) document). If they are not provided there, [contact Pawsey helpdesk](help@pawsey.org.au) first to see if they can add them to the shared folder. If not, proceed with the installation yourself using the instructions below.
#### Lyra
Check with the [eResearch team](https://www.qut.edu.au/research/eresearch) if Lyra has a shared repository of references. If not, proceed with the installation yourself (below).

## Download databases if they are not provided
### BLAST nucleotide sequence database (NT)
The following command will create a script ```download_blastdb.sh``` that downloads a perl script update_blastdb.pl, which will download and decompress all the necessary latest components of the NT database. The scheduler directives will depend on your HPC (see instructions below).  After creating the script `download_blastdb.sh`, you will need to submit it to the scheduler. The command will also depend on the scheduler the HPC uses - refer to the section below to find the appropriate command.
{% include callout.html type="note" content="Make sure to create a folder where you will store the database first and then change the paths before you execute the command." %}
```bash
cat <<EOF > download_blastdb.sh
#!/bin/bash -l
<DIRECTIVES SPECIFIC TO THE SCHEDULER ON YOUR HPC>

cd <FULL PATH TO WHERE YOUR DATABASE WILL BE STORED>
curl -sO ftp://ftp.ncbi.nlm.nih.gov/blast/temp/update_blastdb.pl
chmod +x update_blastdb.pl
perl update_blastdb.pl --decompress nt
perl update_blastdb.pl taxdb
tar -xzf taxdb.tar.gz
EOF
```

#### Gadi
##### Directives specific to PBS on Gadi
```bash
#PBS -N d_blastdb
#PBS -l mem=60gb
#PBS -l walltime=08:00:00
#PBS -q copyq
```
##### Command to submit the script to PBS
```bash
qsub download_blastdb.sh
```
#### Setonix
##### Directives specific to Slurm on Setonix
```bash
#SBATCH --job-name=d_blastdb
#SBATCH --mem=60gb
#SBATCH --time=08:00:00
```
##### Command to submit the script to Slurm
```bash
sbatch download_blastdb.sh
```
#### Lyra
##### Directives specific to PBS on Lyra
```bash
#PBS -N d_blastdb
#PBS -l mem=60gb
#PBS -l walltime=08:00:00
```
##### Command to submit the script to PBS
```bash
qsub download_blastdb.sh
```

### Kraken
The following command will create a script ```download_kraken.sh``` which will download and decompress the [Kraken2-compatile pre-built index](https://benlangmead.github.io/aws-indexes/k2) PlusPFP (version from 10/09/2023) that contains Refeq archaea, bacteria, viral, plasmid, human, UniVec_Core plus Refeq protozoa, fungi & plant.  
{% include callout.html type="note" content="Make sure to create a folder where you will store the database first and then change the paths before you execute the command. Change the version as well if necessary." %}
```bash
cat <<EOF > download_kraken.sh
#!/bin/bash -l
<DIRECTIVES SPECIFIC TO THE SCHEDULER ON YOUR HPC>

cd <FULL PATH TO WHERE YOUR DATABASE WILL BE STORED>
wget https://genome-idx.s3.amazonaws.com/kraken/k2_pluspf_20231009.tar.gz
mkdir -p k2_pluspf_20231009
tar -zxvf k2_pluspf_20231009.tar.gz -C  k2_pluspf_20231009
EOF
```
After creating the script `download_kraken.sh`, submit it to the scheduler. The command will depend on the scheduler the HPC uses - refer to the section below to find the appropriate command.
#### Gadi
##### Directives specific to PBS on Gadi
```bash
#PBS -N d_kraken
#PBS -l mem=60gb
#PBS -l walltime=08:00:00
#PBS -q copyq
```
##### Command to submit the script to PBS
```bash
qsub download_kraken.sh
```
#### Setonix
##### Directives specific to Slurm on Setonix
```bash
#SBATCH --job-name=d_kraken
#SBATCH --mem=60gb
#SBATCH --time=08:00:00
```
##### Command to submit the script to Slurm
```bash
sbatch download_kraken.sh
```
#### Lyra
##### Directives specific to PBS on Lyra
```bash
#PBS -N d_kraken
#PBS -l mem=60gb
#PBS -l walltime=08:00:00
```
##### Command to submit the script to PBS
```bash
qsub download_kraken.sh
```

### Kaiju
The following command will create a script ```download_kaiju.sh``` which will download and decompress the [Kaiju-compatible pre-built index](https://bioinformatics-centre.github.io/kaiju/downloads.html) for protein sequences from [the Reference Viral Databases (RVDB-prot)]https://rvdb-prot.pasteur.fr/) v26.0 database.
{% include callout.html type="note" content="Make sure to create a folder where you will store the database first and then change the paths before you execute the command. Change the version as well if necessary." %}
```bash
cat <<EOF > download_kaiju.sh
#!/bin/bash -l
<DIRECTIVES SPECIFIC TO THE SCHEDULER ON YOUR HPC>

cd <FULL PATH TO WHERE YOUR DATABASE WILL BE STORED>
wget https://kaiju-idx.s3.eu-central-1.amazonaws.com/2023/kaiju_db_rvdb_2023-05-26.tgz
tar -zxvf kaiju_db_rvdb_2023-05-26.tgz
EOF
```
After creating the script `download_kaiju.sh`, submit it to the scheduler. The command will depend on the scheduler the HPC uses - refer to the section below to find the appropriate command.
#### Gadi
##### Directives specific to PBS on Gadi
```bash
#PBS -N d_kaiju
#PBS -l mem=60gb
#PBS -l walltime=08:00:00
#PBS -q copyq
```
##### Command to submit the script to PBS
```bash
qsub download_kaiju.sh
```
#### Setonix
##### Directives specific to Slurm on Setonix
```bash
#SBATCH --job-name=d_kaiju
#SBATCH --mem=60gb
#SBATCH --time=08:00:00
```
##### Command to submit the script to Slurm
```bash
sbatch download_kaiju.sh
```
#### Lyra
##### Directives specific to PBS on Lyra
```bash
#PBS -N d_kaiju
#PBS -l mem=60gb
#PBS -l walltime=08:00:00
```
##### Command to submit the script to PBS
```bash
qsub download_kaiju.sh
```

### VirDB
VirDB is a database created by the QUT eResearch team by merging GenBank, RefSeq and NCBI virus sequences and collapsing those with 99% similarity.<br>
The following command will create a script, ```download_virdb.sh```, which will download and decompress [this collection of viral sequences](https://zenodo.org/records/10183620).

{% include callout.html type="note" content="Make sure to create a folder where you will store the database first and then change the paths before you execute the command. Change the version as well if necessary." %}
```bash
cat <<EOF > download_virdb.sh
#!/bin/bash -l
<DIRECTIVES SPECIFIC TO THE SCHEDULER ON YOUR HPC>

cd <FULL PATH TO WHERE YOUR DATABASE WILL BE STORED>
https://zenodo.org/records/10183620/files/VirDB_20230913.tar.gz
tar -zxvf VirDB_20230913.tar.gz
EOF
```
After creating the script `download_virdb.sh`, submit it to the scheduler. The command will depend on the scheduler the HPC uses - refer to the section below to find the appropriate command.
#### Gadi
##### Directives specific to PBS on Gadi
```bash
#PBS -N d_virdb
#PBS -l mem=60gb
#PBS -l walltime=08:00:00
#PBS -q copyq
```
##### Command to submit the script to PBS
```bash
qsub download_virdb.sh
```
#### Setonix
##### Directives specific to Slurm on Setonix
```bash
#SBATCH --job-name=d_virdb
#SBATCH --mem=60gb
#SBATCH --time=08:00:00
```
##### Command to submit the script to Slurm
```bash
sbatch download_virdb.sh
```
#### Lyra
##### Directives specific to PBS on Lyra
```bash
#PBS -N d_virdb
#PBS -l mem=60gb
#PBS -l walltime=08:00:00
```
##### Command to submit the script to PBS
```bash
qsub download_virdb.sh
```
