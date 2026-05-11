# NetRare
A reproducible network-based bioinformatics framework for molecular signature characterization and gene prioritization in rare diseases.

## Features

- Protein-protein interaction network construction using STRINGdb
- Functional and physical interaction filtering (score ≥400 / ≥900)
- Network topology analysis with igraph/tidygraph
- GO Biological Process and KEGG enrichment analysis
- Gene prioritization using topology and random walk propagation
- Functional module detection and annotation
- Automated comparative visualizations
- Reproducible HTML report generation

## Project Structure
```text
NetRare/
├── README.md
├── main.R
├── environment.yml
├── Dockerfile
├── Snakefile
│
├── data/
│   ├── disease_pairs.tsv
│   ├── genes_CMD_from_HPO.tsv
│   └── genes_CM_from_HPO.tsv
│
├── scripts/
│   ├── build_network.R
│   ├── analyze_network.R
│   ├── run_enrichment.R
│   ├── prioritize_yatra.R
│   └── compare_diseases.R
│
├── output/
│   ├── CMD/
│   ├── CM/
│   └── comparison/
│
├── reports/
│   ├── CMD_CM_report.html
│   └── report_template.Rmd
│
├── figures/
│
└── docs/
```
## Tech Stack

- R
- Python
- Snakemake
- STRINGdb
- clusterProfiler
- igraph
- tidygraph
- ggraph
- Bioconductor
- Conda

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/SDmD6/NetRare.git
cd NetRare
```

### 2. Create the conda environment

```bash
conda env create -f environment.yml
conda activate netrare
```

### 3. Install Bioconductor dependencies

```r
if (!requireNamespace("BiocManager", quietly = TRUE)) {
  install.packages("BiocManager")
}

BiocManager::install(c(
  "STRINGdb",
  "clusterProfiler",
  "org.Hs.eg.db"
))
```
## Usage

Edit the disease comparison file:

```text
data/disease_pairs.tsv
```

Run the full pipeline:

```bash
Rscript main.R
```

Generate the HTML report:

```r
source("scripts/generate_report.R")
```

Main results are generated in:

```text
output/
```

## References

- STRING: https://string-db.org
- HPO: https://hpo.jax.org
- clusterProfiler: https://bioconductor.org/packages/clusterProfiler
- Yatra: https://github.com/TranslationalBioinformaticsLab/yatra

## Citation

Developed as part of an MSc Bioinformatics thesis focused on reproducible network-based analysis of rare diseases.
