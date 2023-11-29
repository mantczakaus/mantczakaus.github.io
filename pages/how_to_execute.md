---
title: How to execute ONTvisc pipeline
toc: false
---



## Launch Tower Agent
#### Gadi and Setonix (HPC)
You need to start Tower Agent so that it is able to pick up the pipeline job when you launch it in Nextflow Tower. Follow instructions in the [How to set up/Launch Tower Agent](https://mantczakaus.github.io/ontvisc_guide/how_to_setup#launch-tower-agent) portion of the guide.

## Create a folder to which you will direct the execution of the pipeline
#### Gadi and Setonix (HPC)
You had to specify the `Work directory` (and optionally, the `Launch directory`) when you were [adding the Compute Environment](https://mantczakaus.github.io/ontvisc_guide/how_to_setup#add-a-compute-environment). Make sure these folders exist on the HPC. 
#### Lyra (HPC)
Create folders where all the task work directories will be created (`Work directory`) and all the execution scripts, config files and logs will be stored (`Launch directory`). More information in the [How to set up/Add a Compute Environment](https://mantczakaus.github.io/ontvisc_guide/how_to_setup#add-a-compute-environment) portion of the guide.

## Launch the pipeline with the `test` configuration
#### Gadi and Setonix (Nextflow Tower)
In the Launchpad, select the ONTvisc pipeline you added in the [How to set up/Add a pipeline](https://mantczakaus.github.io/ontvisc_guide/how_to_setup#add-a-pipeline) portion of the guide and click `Launch`. You need to modify two fields before you click `Launch`.
##### Config profiles
Add the profile `test` in addition to `singularity`.
##### Pipeline parameters
When `test` configuration is used, you do not need to specify any parameters. However, it is recommended to specify the folder where the results are stored. Copy and paste the following command and replace the directory.
```
outdir: <PATH WHERE YOU WANT THE RESULTS TO BE STORED>
```
{% include callout.html type="note" content="Pipeline parameters can be parsed in the JSON or YAML format. The `outdir` above is parsed in the YAML format. Examples can be found in the [CLI/run/Examples](https://www.nextflow.io/docs/latest/cli.html#run) portion of the Nextflow guide." %}
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

cd $PBS_O_WORKDIR
module load java
NXF_OPTS='-Xms1g -Xmx4g'

nextflow run eresearchqut/ontvisc \
	-profile singularity,test \
	--outdir <PATH WHERE YOU WANT THE RESULTS TO BE STORED>

EOF
```
Submit the script to the PBS scheduler by executing the command `qsub submit_test.sh`.

## Monitoring
### Nextflow Tower
#### Gadi, Setonix and Lyra
Tips on monitoring in the [Seqera's guide for Nextflow Tower](https://help.tower.nf/23.2/monitoring/overview/)
### HPC
#### Gadi and Lyra
Execute the `qstat -u <user-name>` to see the progress of the pipeline.
#### Setonix
Execute the `squeue -u <user-name>` to see the progress of the pipeline.

## Relaunching and resuming
#### Nextflow Tower
Tips on relaunching and resuming the pipeline in the [Seqera's guide for Nextflow Tower](https://help.tower.nf/23.2/launch/launchpad/#relaunch-pipeline-run)
#### HPC
If you need to relaunch the pipeline, just re-submit the script. Tips on resuming can be found in the two blog posts from Nextflow: [Troubleshooting Nextflow resume](https://www.nextflow.io/blog/2019/troubleshooting-nextflow-resume.html) and [Demystifying Nextflow resume](https://www.nextflow.io/blog/2019/demystifying-nextflow-resume.html).

## Results
