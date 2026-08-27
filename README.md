# MPXV Washington Focused Build

## Build Overview
- **Build Name**: MPXV Washington Focused Build
- **Pathogen/Strain**: MPXV/Monkeypox Virus/MPOX
- **Scope**: Whole genome, IIb clade
- **Purpose**: This repository contains the Nextstrain build for Washington State genomic surveillance of MPOX clade IIb. The purpose of this Nextstrain build is to monitor and analyze the genetic variations and spread of the MPOX virus within the Washington state region. By utilizing genomic sequencing data, this build helps track the lineage and evolution of the virus, facilitating early detection of any emerging variants. It ultimately aids public health officials in understanding and responding to the outbreak, ensuring that interventions are informed by the latest science.
- **Considerations**: The Washington-focused MPOX build is located within the phylogenetic folder of the Nextstrain MPOX build. This document will explain the components of the Global MPOX build and its dependencies that the Washington-focused build relies on, as well as the dependencies specific to the Washington-focused build, providing necessary context and clarity.  


- **Nextstrain Build/s Location/s**: https://nextstrain.org/groups/wadoh/mpox/wa

## Table of Contents
- [Pathogen Epidemiology](#pathogen-epidemiology)
- [Scientific Decisions](#scientific-decisions)
- [Getting Started](#getting-started)
  - [Data Sources & Inputs](#data-sources--inputs)
  - [Setup & Dependencies](#setup--dependencies)
    - [Installation](#installation)
    - [Clone the repository](#clone-the-repository)
- [Run the Build](#run-the-build-with-test-data)
  - [Expected Outputs](#expected-outputs)
  - [Visualizing Results](#visualize-results)
- [Customization for Local Adaptation](#customization-for-local-adaptation)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements](#acknowledgements)

## Pathogen Epidemiology
 ### Overview
  - #### Pathogen type and family:
    - Monkeypox virus (MPXV) is a double-stranded DNA virus belonging to the genus Orthopoxvirus within the family Poxviridae.
    - It is closely related to variola virus (the causative agent of smallpox), vaccinia virus, and cowpox virus.
  - #### Key subtypes/lineages relevant to the build:
    - As of 2025, three primary clades of MPXV are recognized:
      - Clade I (Congo Basin clade): Found predominantly in Central Africa. Historically associated with severe disease and case fatality rates up to 10%. Transmission is primarily zoonotic, with limited human-to-human spread.
      - Clade IIa (West African clade): Circulates in West Africa, characterized by lower virulence and mortality; transmission is mostly zoonotic.
      - Clade IIb (Global human-to-human clade): Responsible for the global outbreak beginning in May 2022, including the cases detected in Washington State. This clade has demonstrated sustained human-to-human transmission and is the primary focus of the Washington Nextstrain build.
  - #### Mode(s) of transmission:
    - MPXV spreads through close contact with infected individuals or animals, contaminated materials (such as bedding or clothing), respiratory droplets, and exposure to lesion exudates. In recent global outbreaks, human-to-human transmission has been driven largely by close physical or sexual contact, often within interconnected social networks.

  - #### Nomenclature:
    - WHO and global partners transitioned from region-based clade naming to a numeric system in 2022 to reduce stigmatization. Under this system, Clade I replaces “Central African,” Clade IIa replaces “West African,” and Clade IIb denotes the current outbreak lineage, often associated with the hMPXV-1 designation.
    - The Nextstrain MPXV build follows this updated nomenclature for lineage assignment and visualization.

### Geographic Distribution and Seasonality
  - #### Global distribution:
    - MPXV was historically endemic to parts of Central and West Africa, maintained in small mammal reservoirs. Since 2022, Clade IIb has spread globally, with sustained transmission in North America, Europe, and other regions outside of Africa. Sporadic introductions and local clusters continue to be reported worldwide.

  - #### Regional context (Washington State):
    - Washington has reported multiple cases since 2022, primarily linked to domestic transmission of Clade IIb lineages. The Washington State Department of Health continues to monitor genetic diversity within the state to identify introductions, trace connections between cases, and detect signs of local persistence.

  - #### Seasonality:
    - Historically, MPXV transmission in endemic regions exhibits weak seasonality, often aligning with increased human–animal contact during dry seasons. In the context of global Clade IIb transmission, cases occur year-round, influenced more by behavioral and network factors than by environmental seasonality.

### Public Health Importance
  - Mpox remains a nationally notifiable condition and an emerging zoonotic and sexually associated infectious disease of concern. Ongoing genomic surveillance is critical to:
    - Detect new introductions and sustained community transmission in Washington.
    - Monitor for mutations that could influence transmissibility, virulence, or immune escape.
    - Support targeted public health interventions, vaccination strategies, and contact tracing efforts.
  - Sustained genomic monitoring also ensures rapid detection of any novel Clade IIb sublineages that could differ in clinical presentation, response to antivirals, or vaccine effectiveness.

### Genomic Relevance
  - Genomic sequencing and phylogenetic analysis are essential tools for MPXV surveillance. They enable:
    - Detection of lineage shifts to identify newly emerging clades or introductions.
    - Tracking of transmission chains across regions or clusters.
    - Support for outbreak investigations, particularly where epidemiologic links are uncertain.
    - Monitoring of vaccine escape and antiviral resistance, especially given the use of smallpox-based vaccines (e.g., JYNNEOS).
    - Understanding of evolutionary mechanisms, such as APOBEC3-mediated G→A mutation patterns observed in Clade IIb viruses, which may contribute to adaptation and ongoing human transmission.
  - The Washington-focused Nextstrain build integrates these genomic insights into a regional context to assist public health response and inform cross-jurisdictional coordination.

### Additional Resources
  - CDC Mpox Overview: https://www.cdc.gov/mpox/

  - WHO Mpox Factsheet: https://www.who.int/news-room/fact-sheets/detail/mpox

  - Nextstrain Global MPXV Build: https://nextstrain.org/monkeypox/hmpxv1

  - Scientific Background: Gigante et al., 2023, Emerging Infectious Diseases – “Multiple Lineages of Monkeypox Virus Detected During the 2022 Outbreak.”

## Scientific Decisions
Nextstrain builds are designed for specific purposes and not all types of builds for a particular pathogen will answer the same questions. The following are critical decisions that were made during the development of this build that should be kept in mind when analyzing the data and using this build.

- **Subsampling**: 
The subsampling strategy for the Washington focused build can be located here `mpox/phylogenetic/wa_mpxv/wa_config_hmpxv1.yaml`. The Washington-focused build filters out samples before 2017 and those with less than 100,000 base pairs. It then organizes the remaining samples by division year, with 500 sequences in each group, while excluding samples that are not from Washington state. In contrast, the Global build categorizes sequences by lineage, also with 500 sequences per group, and excludes samples from Washington and those not belonging to the IIb clade. The Washington-focused build subsequently combines these datasets for use in the final build.

  Washington Focused MPOX Build Subsampling Schema:
    group_by: "--group-by division year"
    sequences_per_group: "--sequences-per-group 500"
    other_filters: "--exclude-where division!=Washington"

  Global MPOX Build Subsampling Schema:
    group_by: "--group-by lineage"
    sequences_per_group: "--subsample-max-sequences 500"
    other_filters: "--exclude-where division=Washington outbreak!=hMPXV-1 clade!=IIb"

- **Root selection**: 
In the Global MPOX build, MK783032 and MK783030 are utilized to establish the root of the tree, with MK783032 serving as the root for the Washington MPOX build. These root sequences were selected due to problems encountered when the build attempted to determine its own root. MK783030 and MK783032 were identified as the most suitable samples for rooting the tree due to their more uniform appearance. The samples were likely selected based on their clock rates, possibly using BEAST to assess these rates. It was important for the samples to be distinct from the A.1 and B.1 clades as the B.1 clade likely exhibits a higher clock rate. Generally, Clade I viruses exhibit slower clock rates when compared to Clade II. Notably, MK783032 completely outgroups MK783030.

- **Reference selection**:
NCBI Reference Sequence: NC_063383.1
https://www.ncbi.nlm.nih.gov/nuccore/NC_063383.1/
Monkeypox virus, complete genome
LOCUS       NC_063383             197209 bp    DNA     linear   VRL 18-NOV-2022
The reference sequence is identical to MT903340.
The sequence was isolate from a human, within Rivers State, Nigeria and belongs to MPXV clade 2.

- **Inclusion/Exclusion**: 
Rooting sequences MK783032 and MK783030 are included in the include.txt file, located here `mpox\phylogenetic\wa_mpxv`. 

Samples that have been excluded from the Global MPXV build and subsequently the Washington focused build are located here, `mpox/phylogenetic/defaults/exclude_accessions.txt`. The excluded sequences consist of potential recombinants, duplicate sequences, those that do not align well, and highly divergent sequences, as well as overdiverged sequences or those with questionable clusters. Additional filtering criteria for exclusions include sequences from before 2017 and those that do not meet the minimum length requirement of 185,000 base pairs.

## Getting Started
Some high-level features and capabilities specific to this build include:

- **G -> A or C -> T Fraction:** The G → A or C → T fraction refers to the proportion of specific types of nucleotide mutations in a sequence of DNA or RNA. Specifically, it denotes the frequency or occurrence of mutations where guanine (G) changes to adenine (A) or cytosine (C) changes to thymine (T). 
  - These mutations are often studied in the context of genetic variation and evolution, as they can impact the function of genes and the characteristics of organisms over time. In genomic studies, understanding the G → A and C → T mutations can give insights into evolutionary processes, disease mechanisms, and the dynamics of epidemics. 
  - Mutations from G to A or C to T are thought to have played a role in the escaping drift loss, which contributed to the evolution of MPXV seen in the ongoing epidemic.

- **NGA/TCN Context of G -> A/C:** The term "NGA/TCN" refers to specific contexts in which nucleotide mutations occur, particularly in relation to the positions surrounding the nucleotides being mutated. 
  - NGA indicates that the guanine (G) is preceded by any nucleotide (N can be A, T, C, or G) and is followed by adenine (A).
  - TCN indicates that the nucleotide preceding the change (which is usually a guanine in this case) is cytosine (C) and is followed by any nucleotide (N can also be A, T, C, or G).
  - In the context of mutations from G to A or G to C, examining these specific nucleotide contexts can provide insights into how mutations arise and their potential effects on the function of genes. This approach is often used in evolutionary biology and genetics to understand patterns of mutations and their implications in various biological processes, including in the study of viruses like MPXV.
 

### Data Sources & Inputs
How Samples are Ingested from NCBI: `mpox/ingest/rules/fetch_from_ncbi.smk`
How Samples are Prepared for Sequencing: `mpox/phylogenetic/rules/prepare_sequences.smk`

This build relies on publicly available data sourced from data.nextstrain.org which originates from NCBI. This data is generously shared by labs around the world and deposited in NCBI genbank by the authors. Please contact these labs first if you plan to publish using their data. 

MPXV sequences and metadata can be downloaded in the `/ingest` folder using
`nextstrain build --cpus 1 ingest` or `nextstrain build --cpus 1 .` if running directly from the `/ingest` directory.

- **Expected Inputs**:
    - `mpox/phylogenetic/data/sequences.fasta.xz` is decrompressed for a final output of `mpox/phylogenetic/data/sequences.fasta` (containing viral genome sequences)
    - `mpox/phylogenetic/data/metadata.tsv.gz` is decompressed for a final output of `mpox/phylogenetic/data/metadata.tsv` (with relevant sample information)

### Setup & Dependencies
#### Installation
Ensure that you have [Nextstrain](https://docs.nextstrain.org/en/latest/install.html) installed.

To check that Nextstrain is installed:
```
nextstrain check-setup
```
#### Clone the repository:

```
git clone https://github.com/NW-PaGe/mpox.git
```

## Run the Build With Test Data
To test the pipeline with the provided example data located in `mpox/phylogenetic/example_data` make sure you are located in the build folder `mpox/phylogenetic/example_data` before running the build command:
If you want to use this test data, move it to "this" folder. 
```
nextstrain build .
```

When you run the build using `nextstrain build .`, Nextstrain uses Snakemake as the workflow manager to automate genomic analyses. The Snakefile in a Nextstrain build defines how raw input data (sequences and metadata) are processed step-by-step in an automated way. Nextstrain builds are powered by Augur (for phylogenetics) and Auspice (for visualization) and Snakemake is used to automate the execution of these steps using Augur and Auspice based on file dependencies.

## Run the Build
Ensure you are in the `mpox/phylogenetic` folder when running this build.
```
 nextstrain build --cpus 6 . --configfile wa_mpxv/wa_config_hmpxv1.yaml
```

## Expected Outputs
After successfully running the build there will be two output folders containing the build results.

- `auspice/` folder contains `mpox_wa.JSON` and `mpox_wa_root_sequence.JSON`
- `results/` folder contains `hmpxv1_wa/`
  - [Link to `results` folder wiki](https://github.com/NW-PaGe/mpox/wiki/results)

For more detailed information on the complete file structure of this repo please refer to our [wiki](https://github.com/NW-PaGe/mpox/wiki) 

## Visualizing Results
Once your build completes successfully, the results can be explored using Nextstrain Auspice, either locally or on the Nextstrain web platform.

### Local Visualization
To view the resulting phylogenetic tree and metadata locally:
```
nextstrain view auspice/
```
This command launches a local Auspice web server and opens your default web browser to display the Washington-focused MPOX build.
You should see a URL such as:
http://127.0.0.1:4000/

### Interacting with the Visualization
- Tree view: Displays the inferred evolutionary relationships among Washington and global MPXV genomes.
- Map view: Shows the geographic spread of sequences, highlighting Washington-specific samples.
- Entropy panel: Indicates genome regions with higher mutation rates.
- Color by attributes: Use the sidebar to color nodes by variables such as lineage, collection date, clade, or division.
- Filters and search: Restrict the dataset to specific time frames, divisions, or lineages to focus on regional dynamics.

## Customization for Local Adaptation
This build can be customized for use by other states, cities, counties, or countries. By utilizing the Washington focused folder model, `mpox/phylogenetic/wa_mpxv`, and altering specifications within the files to meet your needs, the Global MPXV Nextstrain build can be tailored to fit your requirements. The following steps are recommendations on how to easily alter the build to meet your adaptations:
- Create a folder for your build in `mpox/phlogenetic`. 
- Copy over the files in `mpox/phylogenetic/wa_mpxv` into your folder.
- In your folder, start to alter the following files to meet your needs. Use the dropdown arrows to expand on what areas of the file you may want to change:
  - <details><summary><code> wa_auspice_config_hmpxv1.json</code>: Alter how your build will look.</summary> 
    - <code>title</code>
    <br>
    - <code>maintainers</code>
    <br>
    - <code>build_url</code></details>
   
  - <details><summary><code> wa_config_hmpxv1.yaml</code>: Alter the filtering and sampling of your build.</summary>
      - <code>auspice_config</code>
      <br>
      - <code>description</code>
      <br>
      - <code>build_name</code>
      <br>
      - <code>auspice_name</code>
      <br>
      - <code>filter</code>
      <br>
      - <code>subsample</code>
      <br>

  - `wa_description.md`: Alter your builds description

## Contributing
For any questions please submit them to our [Discussions](https://github.com/orgs/NW-PaGe/discussions/categories/q-a) otherwise software issues and requests can be logged as a Git [Issue](https://github.com/NW-PaGe/wa_mpxv/issues).

## License
This project is licensed under a modified GPL-3.0 License.
You may use, modify, and distribute this work, but commercial use is strictly prohibited without prior written permission.

## Acknowledgements 
We gratefully acknowledge the contributions of the AMD teams (Microbiology, MEP, Bioinformatics, DIQA), Washington State Public Health Laboratories (WA PHL), and our colleagues at the Washington State Department of Health, whose expertise and dedication made this work possible. We also extend our sincere thanks to the Nextstrain development team for their ongoing collaboration and support.
