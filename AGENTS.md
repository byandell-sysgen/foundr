# foundr — Project Memory

## Overview

**foundr** is an R package (v1.5.0) by Brian S. Yandell (UW-Madison)
for analyzing and visualizing multiparent founder study data, particularly
from Collaborative Cross (CC) mouse crosses.
It provides tools for studying genetic variation, phenotypic traits,
and statistical contrasts across founder strains.

**License:** GPL-3  
**GitHub:** https://github.com/byandell/foundr

## Related Ecosystem

| Repository | Purpose |
|---|---|
| `foundrShiny` | Interactive Shiny web app companion |
| `FounderDietStudy` | Domain-specific diet study application |
| `FounderCalciumStudy` | Domain-specific calcium study application |
| `modulr` | WGCNA module harmonization |

**Live apps:**  
- https://connect.doit.wisc.edu/FounderCalciumStudy/  
- https://connect.doit.wisc.edu/FounderDietStudy/ (password protected)

## Founder Strains

The 8 Collaborative Cross founder strains: AJ, B6, 129, NOD, NZO, CAST, PWK, WSB.  
Colors are in `CCcolors` (Okabe-Ito color-blind friendly palette).

## Primary Data Format

Long-format data frames with columns:

| Column | Description |
|---|---|
| `dataset` | Data source identifier |
| `strain` | Founder strain (one of 8 CC strains) |
| `sex` | Biological sex (M/F) |
| `animal` | Individual identifier |
| `condition` | Experimental condition (optional) |
| `trait` | Phenotypic trait name |
| `value` | Measured trait value |

Processed data also includes: `signal`, `cellmean`,
`p.value`, `SD`, `term`.

**Built-in example data:** `sampleData`, `CCcolors`, `EnrichData`,
`EnrichSignal`, `EnrichStats`

## Typical Analysis Workflow

1. Load data in long format
2. `partition()` — decompose trait values into orthogonal signal/rest/noise
components
3. `strainstats()` — compute strain×sex×condition statistical summaries
(ANOVA/linear models)
4. `traitSolos()` / `traitPairs()` / `traitTimes()` — select and
structure traits for analysis
5. `bestcor()` — identify top correlated traits (Spearman)
6. `plot()` / `autoplot()` / `ggplot_*()` — visualize results

## Key Function Groups

### Data Analysis
- `partition()` — orthogonal decomposition of variance
- `strainstats()` — strain/sex/condition stats with F-statistics and p-values
- `conditionContrasts()` — contrasts between experimental conditions
- `bestcor()` — best Spearman correlations between traits
- `eigen_cor()`, `eigen_contrast()` — eigentrait correlation/contrast
- `traitAncova()` — ANCOVA analysis

### Trait Objects (with S3 methods)
- `traitSolos` — single-trait analysis
- `traitPairs` — paired-trait relationships
- `traitTimes` — time-course analysis
- `conditionContrasts` — condition contrast summaries
- S3 methods: `autoplot()`, `summary()`, `plot()`, `subset()`, `split()`, `c()`

### Module Analysis (WGCNA integration)
- `module_kMEs()`, `module_band()`, `wgcnaModules()`, `listof_wgcnaModules()`

### Visualization
- `ggplot_template()` — master template for consistent aesthetics
- `ggplot_traitSolos()`, `ggplot_traitPairs()`, `ggplot_traitTimes()`
- `volcano()` — effect size vs. significance
- `ggplot_evidence_spread()` — spread/evidence plots
- `ggplot_bestcor()` — correlation dot plots
- `biplot_signal()`, `biplot_stat()`, `biplot_pca()` — PCA/biplot
(uses `ordr` package)
- `ggplot_conditionContrasts()`

### Utilities
- `nqrank()`, `normalscores()` — normal quantile rank transformation
- `area_under_curve()` — AUC over time points
- `unite_datatraits()` — combine dataset and trait names
- `pivot_pair()` — reshape paired data
- `timetraits()`, `separate_time()`, `stats_time()` — time-series trait helpers

## Key Dependencies

```r
# Data manipulation
library(dplyr); library(tidyr); library(tibble); library(purrr)
# Visualization
library(ggplot2); library(cowplot); library(ggrepel); library(ggdendro);
library(ordr)
# Statistics
library(broom)
# I/O
library(readr); library(readxl)
# Interactive
library(shiny); library(plotly); library(DT)
# Time series
library(zoo)
```

## Project Structure

```
foundr/
├── R/               # 45+ source files
├── data/            # sampleData.RData, CCcolors.RData, Enrich*.rds
├── man/             # 50+ .Rd documentation files
├── vignettes/       # foundr.Rmd, foundrShiny.Rmd, Foundr Vignette.pdf
├── inst/
│   ├── examples/    # Example analyses
│   ├── extdata/     # External data
│   └── shinyApp/    # Standalone Shiny app scripts
├── DESCRIPTION
├── NAMESPACE        # 80+ exported functions
└── README.md
```

## Statistical Approach

- **Partitioning:** Linear model decomposition — reduced model fits `rest`
factors; signal is estimated from residuals
- **Design:** Strain × Sex (± Condition) crossed designs
- **Correlation:** Spearman, reported as absolute values or signed
- **Effect size:** Reported in SD units (fold-change equivalent)
- **Module analysis:** Integrates WGCNA kME values for co-expression modules
- **Time-series:** Supports minute-level and weekly measurements;
`area_under_curve()` for summaries
