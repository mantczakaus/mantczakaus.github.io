---
title: ONTViSc pipeline on HPC using Australian Nextflow Seqera Service
toc: false
---


## About this guide
This is a guide outlining how to set up and execute [the ONTViSc pipeline](https://github.com/eresearchqut/ONTViSc) on three high-performance computing systems hosted by Australian research and computing facilities: [Lyra (Queensland University of Technology)](https://eresearchqut.atlassian.net/wiki/spaces/EG/pages/1545143157/Start+using+the+HPC), [Gadi (National Computational Infrastructure)](https://opus.nci.org.au/display/Help/Gadi+User+Guide) and [Setonix (Pawsey)](https://support.pawsey.org.au/documentation/display/US/Setonix+User+Guide). Throughout this guide we will make use of the Australian Nextflow Seqera Service provided to the researchers by [Australian BioCommons](https://www.biocommons.org.au/). 

## ONTViSc (ONT-based Viral Screening for Biosecurity)
ONTViSc is a Nextflow-based bioinformatics pipeline designed to help diagnostics of viruses and viroid pathogens for biosecurity. It takes fastq files generated from either amplicon or whole-genome sequencing using Oxford Nanopore Technologies as input. The pipeline can either: 1) perform a direct search on the sequenced reads, 2) generate clusters, 3) assemble the reads to generate longer contigs or 4) directly map reads to a known reference. The reads can optionally be filtered from a plant host before performing downstream analysis.
![Pipeline](./images/ONTViSc_pipeline.png)

## Please cite this guide as follows
Antczak, M., Gauthier, M., & Capon, P. (2024). ONTViSc pipeline on HPC using Australian Nextflow Seqera Service (Version 1.0) [Computer software]. https://mantczakaus.github.io/ontvisc_hpc_seqera_service_guide/

## References
[ONTViSc pipeline](https://github.com/eresearchqut/ONTViSc)
### Databases and tools
[NCBI NT](https://www.ncbi.nlm.nih.gov/nucleotide/)<br>
[Kraken2-compatile pre-built index](https://benlangmead.github.io/aws-indexes/k2)<br>
[Kaiju-compatible pre-built index](https://bioinformatics-centre.github.io/kaiju/downloads.html)<br>
[Viral database (QUT)](https://zenodo.org/records/10183620)<br>
[Canu publication](https://genome.cshlp.org/content/27/5/722)<br>
[Canu documentation](https://canu.readthedocs.io/en/latest/index.html)
### NCI
[Gadi User Guide/User Account and Project Memberships](https://opus.nci.org.au/display/Help/1.0+User+Account+and+Project+Memberships)
### Pawsey
[Requesting Access to Pawsey Supercomputers](https://support.pawsey.org.au/documentation/display/US/Requesting+Access+to+Pawsey+Supercomputers)
### Australian BioCommons
[The Australian BioCommons Leadership Share (ABLeS)](https://australianbiocommons.github.io/ables/index)<br>
[The Australian Nextflow Seqera Service](https://www.biocommons.org.au/seqera-service)<br>
[User Guide for the Australian Nextflow Seqera Service](https://australianbiocommons.github.io/nextflow-seqera/user-guide/)
### QUT
[Start using the HPC](https://eresearchqut.atlassian.net/wiki/spaces/EG/pages/1545143157/Start+using+the+HPC)<br>
[eResearch team](https://www.qut.edu.au/research/eresearch)
### Seqera
[User guide for the Seqera Platform, v24.1](https://docs.seqera.io/platform/24.1)<br>
[Nextflow documentation](https://www.nextflow.io/docs/latest/index.html)<br>
[Nextflow training](https://training.nextflow.io/)

## Acknowledgements
This work is supported by [Australian BioCommons](https://www.biocommons.org.au/) via funding from [Bioplatforms Australia](https://bioplatforms.com/) and the Queensland Government Research Infrastructure Co-investment Fund (RICF) programme. Bioplatforms Australia is funded by the National Collaborative Research Infrastructure Strategy (NCRIS).

This guide makes use of the [ELIXIR toolkit theme](https://github.com/ELIXIR-Belgium/elixir-toolkit-theme)

{% include image.html file="elixir-toolkit-theme_logo.svg" alt="Elixir Toolkit Theme logo" max-width="15em" %}
