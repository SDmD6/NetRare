# NetRare

This repository contains the code and data needed to characterize and compare gene signatures associated with diseases using network analysis, functional enrichment, and gene prioritization methods.
The tool was developed as part of Sofía Doménech Dauder’s Master’s thesis in Bioinformatics.

## Features

- Protein-protein interaction network construction using STRINGdb
- Functional and physical interaction filtering (score ≥400 / ≥900)
- Network topology analysis with igraph/tidygraph
- GO Biological Process and KEGG enrichment analysis
- Gene prioritization using topology and random walk propagation
- Functional module detection and annotation
- Automated comparative visualizations
- Reproducible HTML report generation

## Estructura del proyecto
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

## Requisitos

- R >= 4.2.0
- Paquetes CRAN y Bioconductor:
  
install.packages(c("tidyverse", "igraph", "ggraph", "tidygraph",
  "pheatmap", "ggvenn", "circlize", "digest", "glue", "fs"))
if (!requireNamespace("BiocManager", quietly = TRUE)) install.packages("BiocManager")
BiocManager::install(c("STRINGdb", "clusterProfiler", "org.Hs.eg.db"))
- Python >= 3.13 con dependencias estándar (numpy, argparse) para Yatra.

## Ejecución
- Edita data/disease_pairs.tsv con las enfermedades a comparar.
- Ejecuta main.R, que cargará los scripts modulares.
- Los resultados se almacenan automáticamente en output/.
- Para generar el informe HTML: source("scripts/generate_report.R")

## Referencias
STRING: https://string-db.org
HPO: https://hpo.jax.org
clusterProfiler: https://bioconductor.org/packages/clusterProfiler
Yatra: https://github.com/TranslationalBioinformaticsLab/yatra

