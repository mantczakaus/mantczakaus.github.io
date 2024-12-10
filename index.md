---
title: How to set up and execute ONTViSc pipeline on HPC
toc: false
---


## About this guide
This is a guide outlining how to set up and execute [ONTViSc pipeline](https://github.com/eresearchqut/ONTViSc) on three Australian high-performance computing systems: [Lyra (QUT)](https://eresearchqut.atlassian.net/wiki/spaces/EG/pages/1545143157/Start+using+the+HPC), [Gadi (NCI)](https://opus.nci.org.au/display/Help/Gadi+User+Guide) and [Setonix (Pawsey)](https://support.pawsey.org.au/documentation/display/US/Setonix+User+Guide). The following versions of the programs were used throughout this guide:

<table border="1" style="border-collapse: collapse;">
    <tr>
        <th style="border: 1px solid;">Program</th>
        <th style="border: 1px solid;">Lyra</th>
        <th style="border: 1px solid;">Gadi</th>
        <th style="border: 1px solid;">Setonix</th>
    </tr>
    <tr>
        <td style="border: 1px solid;">ONTViSC</td>
        <td style="border: 1px solid;" colspan="3">v1.3</td>
    </tr>
    <tr>
        <td style="border: 1px solid;">Seqera Platform</td>
        <td style="border: 1px solid;" colspan="3">v24.1</td>
    </tr>
    <tr>
        <td style="border: 1px solid;">Singularity</td>
        <td style="border: 1px solid;">3.10.2-1</td>
        <td style="border: 1px solid;">3.11.3</td>
        <td style="border: 1px solid;">4.1.0-slurm</td>
    </tr>
    <tr>
        <td style="border: 1px solid;">Java</td>
        <td style="border: 1px solid;">11.0.15.1</td>
        <td style="border: 1px solid;">jdk-17.0.2</td>
        <td style="border: 1px solid;">openjdk-17.0.8.1_1</td>
    </tr>
    <tr>
        <td style="border: 1px solid;">Nextflow</td>
        <td style="border: 1px solid;">24.10.2</td>
        <td style="border: 1px solid;">24.04.1</td>
        <td style="border: 1px solid;">24.04.3</td>
    </tr>
</table>


## ONTViSc (ONT-based Viral Screening for Biosecurity)
ONTViSc is a Nextflow-based bioinformatics pipeline designed to help diagnostics of viruses and viroid pathogens for biosecurity. It takes fastq files generated from either amplicon or whole-genome sequencing using Oxford Nanopore Technologies as input. The pipeline can either: 1) perform a direct search on the sequenced reads, 2) generate clusters, 3) assemble the reads to generate longer contigs or 4) directly map reads to a known reference. The reads can optionally be filtered from a plant host before performing downstream analysis.
![Pipeline](./images/ONTViSc_pipeline.png)

## Acknowledgements

This guide makes use of the [ELIXIR toolkit theme](https://github.com/ELIXIR-Belgium/elixir-toolkit-theme)

{% include image.html file="elixir-toolkit-theme_logo.svg" alt="Elixir Toolkit Theme logo" max-width="15em" %}
 
Thank you to Sarah Beecroft (Pawsey), Matthew Downton (Gadi) and Ziad Al-Bkhetan (Australian BioCommons) for help with testing the pipeline on Gadi and Setonix, as well as for providing valuable information regarding these two high-performance computing environments. Thank you also to the eResearch team from QUT for making it possible to execute the ONTViSc pipeline on Lyra and for all the provided support.
