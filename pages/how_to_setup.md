---
title: How to set up ONTvisc pipeline
toc: false
---

## Access to Biocommons Tower
## Access to HPC


## Create Personal Access Token
#### Lyra, Gadi and Setonix (Nextflow Tower)
You will need the authentication token for running Tower Agent (Gadi, Setonix) and to direct monitoring of the pipeline to Nextflow Tower (Lyra). The authentication token can be created in `Your tokens` section of your profile in Nextflow Tower.<br> 
![Token](./images/token.png) <br>
More information on the authentication can be found in the Nextflow Tower documentation: [Authentication (Seqera)](https://help.tower.nf/23.2/api/overview/#authentication) and [Create Personal Token (Australian BioCommons)](https://australianbiocommons.github.io/tower/user-guide/create_personal_token).


## Add Credentials for Tower Agent
#### Gadi and Setonix (Nextflow Tower)
Tower Agent needs to be run continuously to be able to pick up jobs from Nextflow Tower and execute them on the HPC. It will also display the output log live and reports after its completed. To run Tower Agent on HPC you first need to create credentials for the Tower Agent. They will be used to launch it together with the Personal Access Token you created in the previous step.<br>
If you are part of an organisational workspace, someone might have already created Tower Agent credentials and enabled sharing the agent. If that's not the case, you'll need to create the credentials yourself. Either way go to the Credentials tab in your organisation's workspace, check if Tower Agent credentials exist already, and if not click Add Credentials.<br> 
![Organisation Credentials](./images/credentials_org.png) <br>
You can also created credentials to work in your personal workspace.<br>
![Personal Credentials](./images/credentials_personal.png) <br>
{% include callout.html type="note" content="When you add credentials for Tower Agent from your personal workspace, you will be able to use it only for executing pipelines from your personal workspace launchpad. Similarly, credentials in your organisation workspace apply to pipelines from the organisation workspace." %}
More information on adding the credentials can be found in Nextflow Tower documentation from Australian BioCommons: [Create Tower Agent credentials](https://australianbiocommons.github.io/tower/user-guide/create_tower_agent_credentials).
#### Lyra
You are only allowed to monitor jobs using Nextflow Tower on Lyra and that does not require running the Tower Agent.


### Add Personal Access Token in GitHub
#### Gadi and Setonix (Nextflow Tower)
GitHub is very restrictive about the number of times you can make [API requests](https://docs.github.com/en/rest/overview/rate-limits-for-the-rest-api?apiVersion=2022-11-28) (it happens when you execute a pipeline in Nextflow Tower directly from GitHub repository). You can increase that number when personal access token is used - that's why we recommend creating one and adding it into credentials (below). Instructions on how to generate the authentication token can be found in the GitHub documentation: [Managing your personal access tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).
{% include callout.html type="note" content="You will need a [GitHub account](https://docs.github.com/en/get-started/signing-up-for-github/signing-up-for-a-new-github-account) first." %}
{% include callout.html type="note" content="Copy/securely store the access token from GitHub. You will need it to use it in Nextflow Tower in the next step." %}
#### Lyra
Not applicable.


### Add Credentials for GitHub
#### Gadi and Setonix (Nextflow Tower)
Credentials for GitHub are created in a similar way to credentials for Tower Agent - you need to navigate to Credentials tab and you have an option to add them at the organisation or personal level. However, instead of choosing Tower Agent as Provider, you'll need to choose GitHub. Fill in the rest according to the help text provided under each of the fields.<br> 
![GitHub Credentials](./images/credentials_github.png)
#### Lyra
Not applicable.

### Add a Compute Environment
### Add a pipeline



## Useful links
## Submit scripts to PBS

## Directly on the HPC
### Download databases
Tools in the ONTvisc pipeline compare the reads/clusters/contigs (depending on the mode) to a database or a reference. The explanation of which databases are required to be provided depending on the selected mode and tips on how to install them can be found in the pipeline's wiki page in the <a href="https://github.com/maelyg/ontvisc/wiki/Installation#installing-the-required-indexes-and-references"> Installing the required indexes and references </a> section. Below commands that will download the respective databases on Gadi. Change paths to folders / links / versions if necessary. Make sure you create a folder where you will store all the databases first and update the scripts when necessary.
#### NT - BlastDB
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
#### Kraken
#### Kaiju
#### VirDB
### Download the pipeline and singularity images (if you are planning to use a queue that does not have network connection)

## Run Tower Agent
