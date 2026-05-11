# Comparador de Firmas Moleculares mediante Redes

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
Listado de rutas de carpetas para el volumen S.O.
El n·mero de serie del volumen es 2095-FA49
C:.
ª   .Rhistory
ª   estructura.txt
ª   main.R
ª   README.md
ª   
+---data
ª   ª   disease_pairs.tsv
ª   ª   genes_CMD_from_HPO.tsv
ª   ª   genes_CM_from_HPO.tsv
ª   ª   phenotype_to_genes.txt
ª   ª   
ª   +---training_genes
ª           CMD_input_hash.txt
ª           CMD_training_genes.tsv
ª           CM_input_hash.txt
ª           CM_training_genes.tsv
ª           
+---output
ª   +---CM
ª   ª   +---enrichment
ª   ª   ª       CM_GO_enrichment.tsv
ª   ª   ª       CM_GO_mapping.tsv
ª   ª   ª       CM_GO_unmapped.tsv
ª   ª   ª       CM_KEGG_enrichment.tsv
ª   ª   ª       CM_KEGG_mapping.tsv
ª   ª   ª       CM_KEGG_unmapped.tsv
ª   ª   ª       
ª   ª   +---network
ª   ª   ª       CM_barplot_functional_vs_physical.png
ª   ª   ª       CM_common_genes_functional_physical.txt
ª   ª   ª       CM_gene_overlap_functional_vs_physical.tsv
ª   ª   ª       CM_network_summary.tsv
ª   ª   ª       CM_network_summary_by_kind.tsv
ª   ª   ª       CM_network_summary_comparison.tsv
ª   ª   ª       CM_network_summary_functional.tsv
ª   ª   ª       CM_network_summary_physical.tsv
ª   ª   ª       CM_node_metrics.tsv
ª   ª   ª       CM_node_metrics_functional.tsv
ª   ª   ª       CM_node_metrics_physical.tsv
ª   ª   ª       CM_venn_functional_vs_physical.png
ª   ª   ª       
ª   ª   +---plots
ª   ª   ª       CM_yatra_top20_subnetwork.pdf
ª   ª   ª       CM_yatra_top20_subnetwork.png
ª   ª   ª       
ª   ª   +---prioritization
ª   ª   ª       combined_ranking.tsv
ª   ª   ª       module_genes_top20.tsv
ª   ª   ª       module_summary_top20.tsv
ª   ª   ª       network.tsv
ª   ª   ª       ranking_classic.tsv
ª   ª   ª       training.txt
ª   ª   ª       yatra_ranking.tsv
ª   ª   ª       yatra_run.log
ª   ª   ª       
ª   ª   +---yatra
ª   ª           CM_network.tsv
ª   ª           CM_training.txt
ª   ª           
ª   +---CMD
ª   ª   +---enrichment
ª   ª   ª       CMD_GO_enrichment.tsv
ª   ª   ª       CMD_GO_mapping.tsv
ª   ª   ª       CMD_GO_unmapped.tsv
ª   ª   ª       CMD_KEGG_enrichment.tsv
ª   ª   ª       CMD_KEGG_mapping.tsv
ª   ª   ª       CMD_KEGG_unmapped.tsv
ª   ª   ª       
ª   ª   +---network
ª   ª   ª       CMD_barplot_functional_vs_physical.png
ª   ª   ª       CMD_common_genes_functional_physical.txt
ª   ª   ª       CMD_gene_overlap_functional_vs_physical.tsv
ª   ª   ª       CMD_network_summary.tsv
ª   ª   ª       CMD_network_summary_by_kind.tsv
ª   ª   ª       CMD_network_summary_comparison.tsv
ª   ª   ª       CMD_network_summary_functional.tsv
ª   ª   ª       CMD_network_summary_physical.tsv
ª   ª   ª       CMD_node_metrics.tsv
ª   ª   ª       CMD_node_metrics_functional.tsv
ª   ª   ª       CMD_node_metrics_physical.tsv
ª   ª   ª       CMD_venn_functional_vs_physical.png
ª   ª   ª       
ª   ª   +---plots
ª   ª   ª       CMD_yatra_top20_subnetwork.pdf
ª   ª   ª       CMD_yatra_top20_subnetwork.png
ª   ª   ª       
ª   ª   +---prioritization
ª   ª   ª       combined_ranking.tsv
ª   ª   ª       module_genes_top20.tsv
ª   ª   ª       module_summary_top20.tsv
ª   ª   ª       network.tsv
ª   ª   ª       ranking_classic.tsv
ª   ª   ª       training.txt
ª   ª   ª       yatra_ranking.tsv
ª   ª   ª       yatra_run.log
ª   ª   ª       
ª   ª   +---yatra
ª   ª           CMD_network.tsv
ª   ª           CMD_training.txt
ª   ª           
ª   +---comparison
ª   ª   ª   common_genes.tsv
ª   ª   ª   exclusive_CM.tsv
ª   ª   ª   exclusive_CMD.tsv
ª   ª   ª   exclusive_go_terms_long.tsv
ª   ª   ª   global_overlap_summary.tsv
ª   ª   ª   jaccard_topk_rankings.tsv
ª   ª   ª   kegg_overlap_summary.tsv
ª   ª   ª   network_summary.tsv
ª   ª   ª   prioritized_genes_CM.tsv
ª   ª   ª   prioritized_genes_CMD.tsv
ª   ª   ª   shared_go_terms.tsv
ª   ª   ª   shared_kegg_paths.tsv
ª   ª   ª   top_central_genes.tsv
ª   ª   ª   
ª   ª   +---plots
ª   ª           CMD_corr_yatra_topo.png
ª   ª           CM_corr_yatra_topo.png
ª   ª           
ª   +---enrichment
ª   ª       CMD_GO_enrichment.tsv
ª   ª       CMD_KEGG_enrichment.tsv
ª   ª       CM_GO_enrichment.tsv
ª   ª       CM_KEGG_enrichment.tsv
ª   ª       
ª   +---network
ª   ª       CMD_cluster_descriptions.tsv
ª   ª       CMD_network.tsv
ª   ª       CMD_network_functional.tsv
ª   ª       CMD_network_physical.tsv
ª   ª       CMD_node_metrics.tsv
ª   ª       CM_cluster_descriptions.tsv
ª   ª       CM_network.tsv
ª   ª       CM_network_functional.tsv
ª   ª       CM_network_physical.tsv
ª   ª       CM_node_metrics.tsv
ª   ª       
ª   +---plots
ª   ª       chordplot_kegg_shared.png
ª   ª       CMD_exclusive_network.png
ª   ª       CMD_network_annotated.png
ª   ª       CMD_network_plot.png
ª   ª       CM_exclusive_network.png
ª   ª       CM_network_annotated.png
ª   ª       CM_network_plot.png
ª   ª       common_genes_network.png
ª   ª       degree_distribution.png
ª   ª       degree_vs_betweenness.png
ª   ª       exclusive_go_terms_barplot.png
ª   ª       global_metrics_comparison.png
ª   ª       go_chord_plot.png
ª   ª       go_term_top_significant.png
ª   ª       heatmap_kegg_terms.png
ª   ª       kegg_barplot.png
ª   ª       module_size_comparison.png
ª   ª       network_metrics_comparison.png
ª   ª       shared_network.png
ª   ª       total_nodes_comparison.png
ª   ª       venn_genes.png
ª   ª       venn_genes_CMD_CM.png
ª   ª       venn_go_terms.png
ª   ª       venn_go_terms_CMD_CM.png
ª   ª       venn_kegg_terms.png
ª   ª       
ª   +---_meta
ª           python_freeze.txt
ª           R_sessionInfo.txt
ª           
+---reports
ª       CMD_CM_report.html
ª       report_template.Rmd
ª       
+---scripts
ª   ª   analyze_network.R
ª   ª   build_network.R
ª   ª   check_yatra_results.R
ª   ª   compare_diseases.R
ª   ª   generate_report.R
ª   ª   prioritize_yatra.R
ª   ª   read_input.R
ª   ª   run_enrichment.R
ª   ª   run_enrichment.R.bak
ª   ª   run_random_walk.R
ª   ª   visual_summary.R
ª   ª   
ª   +---yatra
ª       +---prg
ª       ª   ª   prg.py
ª       ª   ª   run_yatra.py
ª       ª   ª   __init__.py
ª       ª   ª   
ª       ª   +---__pycache__
ª       +---randomWalk
ª           ª   randomWalk.py
ª           ª   randomWalk_expression.py
ª           ª   requirements.txt
ª           ª   run_random_walk.py
ª           ª   
ª           +---__pycache__
ª                   randomWalk.cpython-313.pyc
ª                   randomWalk_expression.cpython-313.pyc
ª                   
+---string_data
        9606.protein.aliases.v11.5.txt.gz
        9606.protein.info.v11.5.txt.gz
        9606.protein.links.v11.5.txt.gz

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

