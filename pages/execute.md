---
title: How to execute ONTViSc pipeline with test data and configuration
toc: false
---

## Launch Tower Agent
#### Gadi and Setonix (HPC)
You need to start Tower Agent so that it can pick up the pipeline job when you launch it in the Australian Nextflow Seqera Service. Follow the instructions in the [How to set up/Launch Tower Agent](https://mantczakaus.github.io/ontvisc_hpc_seqera_service_guide/how_to_setup#launch-tower-agent) section of the guide.

## Create a folder to which you will direct the execution of the pipeline
#### Gadi and Setonix (HPC)
You had to specify the `Work directory` (and optionally, the `Launch directory`) when you were [adding the Compute Environment](https://mantczakaus.github.io/ontvisc_hpc_seqera_service_guide/how_to_setup#add-a-compute-environment). Make sure these folders exist on the HPC. 
#### Lyra (HPC)
Create folders where all the task work directories will be placed (`Work directory`), and where all the execution scripts, config files, and logs will be stored (`Launch directory`). More information in the [How to set up/Add a Compute Environment](https://mantczakaus.github.io/ontvisc_hpc_seqera_service_guide/how_to_setup#add-a-compute-environment) section of the guide.

## Launch the pipeline with the `test` configuration
#### Gadi and Setonix (Australian Nextflow Seqera Service)
In the Launchpad, select the ONTViSc pipeline you added in the [How to set up/Add a pipeline](https://mantczakaus.github.io/ontvisc_hpc_seqera_service_guide/how_to_setup#add-a-pipeline) section of the guide and click `Launch`. 
<br>
<img alt="Launchpad" src="./images/launchpad.png">
<br>
You need to modify two fields before you click `Launch`.
##### Config profiles
Add the profile `test` in addition to `singularity`.
##### Pipeline parameters
When a `test` configuration is used, you do not need to specify any parameters. However, specifying the folder where the results will be generated is recommended. Copy and paste the following command and replace the directory.
```
outdir: <PATH WHERE YOU WANT THE RESULTS TO BE STORED>
```
<br>
<img alt="Launch_pipeline" src="./images/launch_pipeline.png" width="400">
<br>
{% include callout.html type="note" content="Pipeline parameters can be parsed in the JSON or YAML format. The `outdir` above is parsed in the YAML format. Examples can be found in the [CLI/run/Examples](https://www.nextflow.io/docs/latest/cli.html#run) section of the Nextflow guide." %}
#### Lyra (HPC)
Create a submission script in the `Launch directory` by copying and pasting the following command into your terminal (change the required paths first).
```bash
cat <<EOF > submit_test.sh
#!/bin/bash -l
#PBS -N test
#PBS -l select=1:ncpus=2:mem=4gb
#PBS -l walltime=24:00:00
#PBS -e <PATH TO THE ERROR FILE>
#PBS -o <PATH TO THE LOG FILE>

module load java
NXF_OPTS='-Xms1g -Xmx4g'

nextflow run eresearchqut/ONTViSc \
	-profile singularity,test \
	--outdir <PATH WHERE YOU WANT THE RESULTS TO BE STORED>

EOF
```
Submit the script to the PBS scheduler by executing the command `qsub submit_test.sh`.

## Monitoring
### Australian Nextflow Seqera Service
#### Gadi, Setonix and Lyra
Tips on monitoring in the [Seqera's guide for the Australian Nextflow Seqera Service](https://docs.seqera.io/platform/24.1/monitoring/overview/)
### HPC
#### Gadi and Lyra
Execute the `qstat -u <user-name>` to see the pipeline's progress.
#### Setonix
Execute the `squeue -u <user-name>` to see the pipeline's progress.

## Relaunching and resuming
#### Gadi and Setonix (Australian Nextflow Seqera Service)
Tips on relaunching and resuming the pipeline in the [Seqera's guide for the Australian Nextflow Seqera Service](https://docs.seqera.io/platform/24.1/launch/cache-resume)
### Lyra (HPC)
If you need to relaunch the pipeline, re-submit the script. Tips on resuming can be found in the two blog posts from Nextflow: [Troubleshooting Nextflow resume](https://seqera.io/blog/troubleshooting-nextflow-resume.html) and [Demystifying Nextflow resume](https://seqera.io/blog/demystifying-nextflow-resume.html).

## Results
The ONTViSc pipeline with the `test` configuration performs de novo assembly of the reads with Canu and compares the assembled contigs to a reference. If the pipeline is completed successfully, you should see the output files on HPC (and in the Australian Nextflow Seqera Service in the case of Gadi and Setonix).
### HPC
#### Gadi, Setonix and Lyra
Follow the [Output files/De novo assembly mode](https://github.com/eresearchqut/ONTViSc/tree/v1.3?tab=readme-ov-file#de-novo-assembly-mode-outputs) section of the ONTViSc pipeline's guide to check what output should be expected.

### Australian Nextflow Seqera Service
#### Gadi and Setonix
Three reports should be generated.
![Reports](.images/reports.png)
