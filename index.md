---
title: DRAFT: How to set up and execute ONTvisc pipeline
toc: false
---


## About 
### ONTViSc (ONT-based Viral Screening for Biosecurity)
[eresearchqut/ontvisc](https://github.com/eresearchqut/ontvisc) is a Nextflow-based bioinformatics pipeline designed to help diagnostics of viruses and viroid pathogens for biosecurity. It takes fastq files generated from either amplicon or whole-genome sequencing using Oxford Nanopore Technologies as input. The pipeline can either: 1) perform a direct search on the sequenced reads, 2) generate clusters, 3) assemble the reads to generate longer contigs or 4) directly map reads to a known reference. The reads can optionally be filtered from a plant host before performing downstream analysis.
![Pipeline](./images/ONTViSc_pipeline.jpeg)
### This guide
In this guide draft you will find instructions on how to set up and execute the ONTvisc pipeline on three high performance computing systems: [Lyra (QUT)](https://eresearchqut.atlassian.net/wiki/spaces/EG/pages/1545143157/Start+using+the+HPC), [Gadi (NCI)](https://opus.nci.org.au/display/Help/Gadi+User+Guide) and [Setonix (Pawsey)](https://support.pawsey.org.au/documentation/display/US/Setonix+User+Guide).

## Acknowledgements

This guide makes use of the [ELIXIR toolkit theme](https://github.com/ELIXIR-Belgium/elixir-toolkit-theme)

{% include image.html file="elixir-toolkit-theme_logo.svg" alt="Elixir Toolkit Theme logo" max-width="15em" %}
 
Thank you to Sarah Beecroft (Pawsey), Matthew Downton (Gadi) and Ziad Al-Bkhetan (Australian BioCommons) for help with testing the pipeline on Gadi and Setonix, as well as providing valuable information regarding  these two high performance computing environments. Thank you to eResearch team from QUT for making possible to execute the ONTvisc pipeline on Lyra and all the provided support.
