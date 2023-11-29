---
title: How to execute ONTvisc pipeline
toc: false
---



## Launch Tower Agent
#### Gadi and Setonix (HPC)
You need to start Tower Agent so that it is able to pick up the pipeline job when you launch it in Nextflow Tower. Follow instructions in the [How to set up/Launch Tower Agent](https://mantczakaus.github.io/ontvisc_guide/how_to_setup#launch-tower-agent) portion of the guide.

## Create a folder to which you will direct the execution of the pipeline
#### Gadi and Setonix
You had to specify the `Work directory` (and optionally, the `Launch directory`) when you were [adding the Compute Environment](https://mantczakaus.github.io/ontvisc_guide/how_to_setup#add-a-compute-environment). Make sure these folders exist on the HPC. 
#### Lyra (HPC)
Create folders where all the task work directories will be created (`Work directory`) and all the execution scripts, config files and logs will be stored (`Launch directory`). More information in the [How to set up/Add a Compute Environment](https://mantczakaus.github.io/ontvisc_guide/how_to_setup#add-a-compute-environment) portion of the guide.

## Launch the pipeline

