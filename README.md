# Within-Host Microevolution and Clonal Selection of Invasive *Staphylococcus aureus* Using Long-Read Population Genomics

##  Project Overview
This project investigates the genomic epidemiology, within-host microevolution, and clonal selection dynamics of *Staphylococcus aureus* transitions from commensal nasal colonization to invasive bloodstream disease. 

Using **Oxford Nanopore Technologies (ONT) long-read sequencing**, I set out to analyze paired isolates obtained from **nine ST-Matched patients** from the study cohort of **S. AUREUS MANUSCRIPT_03**. I am leading this manuscript and did the entire bioinformatic analysis as referenced.
For each patient in this analysis, the dataset captures the clonal diversity of the nasal reservoir alongside a matching invasive isolate:
* **Invasive Reservoir:** 1 Blood Culture (BC) isolate per patient.
* **Nasal Reservoir:** Up to 8 individual colonies cultured from a single Nasopharyngeal Swab (NPS) per patient.

By resolving full bacterial chromosomes and complex mobile genetic elements (MGEs) with long reads, this study aims to determine whether invasive lineages emerge via a random sampling of the nasal population or through a selective bottleneck driven by specific hyper-virulent mutations or MGE acquisitions.


## Study Design & Clonal Architecture
Because *S. aureus* nasal populations can exhibit high heterogeneity, individual patients may harbor multiple distinct Sequence Types (STs). This pipeline selectively groups and analyzes colonies sharing matching STs between the compartments to track subtle within-host microevolution.

## Bioinformatics Pipeline & Tooling
The pipeline is optimized for long-read bacterial population genomics, structured as follows:

### 1. Quality Control & Preprocessing
* **Tool:** `Chopper` (via Conda)
* **Parameters:** Filter out reads `< 1,000 bp` and average quality scores `< Q10`.

### 2. Multi-Locus Sequence Typing (MLST)
* **Tool:** `mlst` (Seemann)
* **Goal:** Verify and map the sequence types of all 18+ isolates to isolate ST-matched pairs.

### 3. De Novo Assembly & Polishing
* **Tools:** `Flye` + `Medaka`
* **Goal:** Construct a high-quality, circularized, reference-grade chromosome for the dominant baseline nasal colony of each patient.

### 4. Variant Calling & Structural Variation Mapping
* **Alignment:** `Minimap2` (aligning invasive BC reads and alternative nasal colony reads to the patient-specific nasal assembly).
* **Variant Callers:** `Clair3` (for high-accuracy SNPs and small Indels) and `Sniffles2` (for resolving large Structural Variants like inversions or deletions).

### 5. Pangenome & Mobile Genetic Element (MGE) Analysis
* **Annotation:** `Bakta` & `Prokka`
* **Pangenome Analysis:** `Panaroo`
* **Goal:** Track the gain/loss of critical *S. aureus* pathogenicity islands (SaPIs), prophages, plasmids, and antibiotic resistance genes (AMR) across colonies.

### 6. Downstream Visualization (R Ecosystem)
* **Packages:** `tidyverse`, `vcfR`, `ggtree`, and `ComplexHeatmap`.
* **Analysis:** Matrix visualization of convergent mutations across all 9 patients to locate recurrently mutated loci during tissue invasion.


## Project Status & Milestones

- [x] Study design and pipeline architecture finalized    
- [x] Repository initialization and environment setup     
- [ ] Raw FASTQ data acquisition & MLST verification `[Ongoing]`
- [ ] Quality Control & *De Novo* Assembly execution
- [ ] Variant Calling & Structural Variant extraction
- [ ] R-based downstream convergence analysis & mapping

## Affiliation & Contact
* **Institution:** Medical Research Council Unit The Gambia at the London School of Hygiene & Tropical Medicine (MRCG at LSHTM)
* **Author:** [Sulayman Sowe]
* **Email:** [ssulayman636@gmail.com]
