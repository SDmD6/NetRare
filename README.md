# NetRare-Comparador de Firmas Moleculares mediante Redes

Este repositorio contiene el código y los datos necesarios para caracterizar y comparar firmas génicas asociadas a enfermedades mediante métodos de análisis de redes, enriquecimiento funcional y priorización de genes.  
La herramienta ha sido desarrollada como parte del Trabajo de Fin de Máster en Bioinformática de Sofía Doménech Dauder.

## Objetivo

Comparar enfermedades raras a partir de sus genes asociados (extraídos de HPO o PanelApp), mediante:

- Construcción de redes de interacción proteica (STRINGdb, con umbrales diferenciados para asociaciones funcionales ≥400 y físicas ≥900).
- Análisis topológico con igraph/tidygraph.
- Enriquecimiento funcional **GO-BP y KEGG** (clusterProfiler).
- Priorización de genes según:
  - Centralidad (grado + betweenness).
  - Random walk clásico y ponderado por expresión (**Yatra**).
- Detección de módulos funcionales (Walktrap + anotación automática).
- Visualizaciones comparativas (20 tipos: venns, heatmaps, chord plots, scatterplots, etc.).
- Generación de informes automáticos (`rmarkdown`).

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

