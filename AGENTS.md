# foundr — Project Memory

## Overview

**foundr** is an R package (v1.5.0) by Brian S. Yandell (UW-Madison) for
analyzing and visualizing multiparent founder study data, particularly
from Collaborative Cross (CC) mouse crosses. It provides tools for
studying genetic variation, phenotypic traits, and statistical contrasts
across founder strains.

**License:** GPL-3  
**GitHub:** <https://github.com/byandell/foundr>

## Related Ecosystem

| Repository            | Purpose                                   |
|-----------------------|-------------------------------------------|
| `foundrShiny`         | Interactive Shiny web app companion       |
| `FounderDietStudy`    | Domain-specific diet study application    |
| `FounderCalciumStudy` | Domain-specific calcium study application |
| `modulr`              | WGCNA module harmonization                |

**Live apps:**  
- <https://connect.doit.wisc.edu/FounderCalciumStudy/>  
- <https://connect.doit.wisc.edu/FounderDietStudy/> (password protected)

## Founder Strains

The 8 Collaborative Cross founder strains: AJ, B6, 129, NOD, NZO, CAST,
PWK, WSB.  
Colors are in `CCcolors` (Okabe-Ito color-blind friendly palette).

## Primary Data Format

Long-format data frames with columns:

| Column      | Description                          |
|-------------|--------------------------------------|
| `dataset`   | Data source identifier               |
| `strain`    | Founder strain (one of 8 CC strains) |
| `sex`       | Biological sex (M/F)                 |
| `animal`    | Individual identifier                |
| `condition` | Experimental condition (optional)    |
| `trait`     | Phenotypic trait name                |
| `value`     | Measured trait value                 |

Processed data also includes: `signal`, `cellmean`, `p.value`, `SD`,
`term`.

**Built-in example data:** `sampleData`, `CCcolors`, `EnrichData`,
`EnrichSignal`, `EnrichStats`

## Typical Analysis Workflow

1.  Load data in long format
2.  [`partition()`](https://byandell-sysgen.github.io/foundr/reference/partition.md)
    — decompose trait values into orthogonal signal/rest/noise
    components
3.  [`strainstats()`](https://byandell-sysgen.github.io/foundr/reference/strainstats.md)
    — compute strain×sex×condition statistical summaries (ANOVA/linear
    models)
4.  [`traitSolos()`](https://byandell-sysgen.github.io/foundr/reference/traitSolos.md)
    /
    [`traitPairs()`](https://byandell-sysgen.github.io/foundr/reference/traitPairs.md)
    /
    [`traitTimes()`](https://byandell-sysgen.github.io/foundr/reference/traitTimes.md)
    — select and structure traits for analysis
5.  [`bestcor()`](https://byandell-sysgen.github.io/foundr/reference/bestcor.md)
    — identify top correlated traits (Spearman)
6.  [`plot()`](https://rdrr.io/r/graphics/plot.default.html) /
    [`autoplot()`](https://ggplot2.tidyverse.org/reference/autoplot.html)
    / `ggplot_*()` — visualize results

## Key Function Groups

### Data Analysis

- [`partition()`](https://byandell-sysgen.github.io/foundr/reference/partition.md)
  — orthogonal decomposition of variance
- [`strainstats()`](https://byandell-sysgen.github.io/foundr/reference/strainstats.md)
  — strain/sex/condition stats with F-statistics and p-values
- [`conditionContrasts()`](https://byandell-sysgen.github.io/foundr/reference/conditionContrasts.md)
  — contrasts between experimental conditions
- [`bestcor()`](https://byandell-sysgen.github.io/foundr/reference/bestcor.md)
  — best Spearman correlations between traits
- [`eigen_cor()`](https://byandell-sysgen.github.io/foundr/reference/eigen_cor.md),
  [`eigen_contrast()`](https://byandell-sysgen.github.io/foundr/reference/eigen_contrast.md)
  — eigentrait correlation/contrast
- [`traitAncova()`](https://byandell-sysgen.github.io/foundr/reference/traitAncova.md)
  — ANCOVA analysis

### Trait Objects (with S3 methods)

- `traitSolos` — single-trait analysis
- `traitPairs` — paired-trait relationships
- `traitTimes` — time-course analysis
- `conditionContrasts` — condition contrast summaries
- S3 methods:
  [`autoplot()`](https://ggplot2.tidyverse.org/reference/autoplot.html),
  [`summary()`](https://rdrr.io/r/base/summary.html),
  [`plot()`](https://rdrr.io/r/graphics/plot.default.html),
  [`subset()`](https://rdrr.io/r/base/subset.html),
  [`split()`](https://rdrr.io/r/base/split.html),
  [`c()`](https://rdrr.io/r/base/c.html)

### Module Analysis (WGCNA integration)

- [`module_kMEs()`](https://byandell-sysgen.github.io/foundr/reference/module_kMEs.md),
  [`module_band()`](https://byandell-sysgen.github.io/foundr/reference/module_band.md),
  `wgcnaModules()`, `listof_wgcnaModules()`

### Visualization

- [`ggplot_template()`](https://byandell-sysgen.github.io/foundr/reference/ggplot_template.md)
  — master template for consistent aesthetics
- [`ggplot_traitSolos()`](https://byandell-sysgen.github.io/foundr/reference/ggplot_traitSolos.md),
  [`ggplot_traitPairs()`](https://byandell-sysgen.github.io/foundr/reference/ggplot_traitPairs.md),
  [`ggplot_traitTimes()`](https://byandell-sysgen.github.io/foundr/reference/traitTimes.md)
- [`volcano()`](https://byandell-sysgen.github.io/foundr/reference/volcano.md)
  — effect size vs. significance
- [`ggplot_evidence_spread()`](https://byandell-sysgen.github.io/foundr/reference/ggplot_evidence_spread.md)
  — spread/evidence plots
- [`ggplot_bestcor()`](https://byandell-sysgen.github.io/foundr/reference/bestcor.md)
  — correlation dot plots
- [`biplot_signal()`](https://byandell-sysgen.github.io/foundr/reference/biplot_pca.md),
  [`biplot_stat()`](https://byandell-sysgen.github.io/foundr/reference/biplot_pca.md),
  [`biplot_pca()`](https://byandell-sysgen.github.io/foundr/reference/biplot_pca.md)
  — PCA/biplot (uses `ordr` package)
- [`ggplot_conditionContrasts()`](https://byandell-sysgen.github.io/foundr/reference/conditionContrasts.md)

### Utilities

- [`nqrank()`](https://byandell-sysgen.github.io/foundr/reference/nqrank.md),
  `normalscores()` — normal quantile rank transformation
- [`area_under_curve()`](https://byandell-sysgen.github.io/foundr/reference/area_under_curve.md)
  — AUC over time points
- [`unite_datatraits()`](https://byandell-sysgen.github.io/foundr/reference/unite_datatraits.md)
  — combine dataset and trait names
- [`pivot_pair()`](https://byandell-sysgen.github.io/foundr/reference/pivot_pair.md)
  — reshape paired data
- [`timetraits()`](https://byandell-sysgen.github.io/foundr/reference/timetraits.md),
  [`separate_time()`](https://byandell-sysgen.github.io/foundr/reference/separate_time.md),
  [`stats_time()`](https://byandell-sysgen.github.io/foundr/reference/stats_time.md)
  — time-series trait helpers

## Key Dependencies

``` r

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

## Statistical Approach

- **Partitioning:** Linear model decomposition — reduced model fits
  `rest` factors; signal is estimated from residuals
- **Design:** Strain × Sex (± Condition) crossed designs
- **Correlation:** Spearman, reported as absolute values or signed
- **Effect size:** Reported in SD units (fold-change equivalent)
- **Module analysis:** Integrates WGCNA kME values for co-expression
  modules
- **Time-series:** Supports minute-level and weekly measurements;
  [`area_under_curve()`](https://byandell-sysgen.github.io/foundr/reference/area_under_curve.md)
  for summaries
