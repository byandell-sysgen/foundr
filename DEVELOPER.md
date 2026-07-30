# Developer Guide for foundr

Welcome to the developer guide for **foundr** (v1.5.0), an R package for
analyzing and visualizing multiparent founder study data (specifically
Collaborative Cross mouse crosses).

This document details package architecture, data models, developer
environment setup, R coding conventions, S3 object patterns, testing
procedures, and release workflows.

------------------------------------------------------------------------

## 1. Ecosystem & Package Architecture

`foundr` serves as the core statistical analysis, data partitioning, and
plotting engine for multiparent founder studies.

### Package Ecosystem

| Package / Repository | Role / Description |
|----|----|
| [foundr](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/README.md) | Core statistical models, orthogonal variance partitioning, S3 trait classes, and `ggplot2` visualizations |
| `foundrShiny` | Companion interactive Shiny web application for exploratory data analysis |
| `modulr` | WGCNA co-expression module harmonization package |
| `FounderDietStudy` | Domain-specific application for diet study data analysis |
| `FounderCalciumStudy` | Domain-specific application for calcium study data analysis |

### Directory Structure

    foundr/
    ├── R/               # Source R functions (partitioning, strainstats, S3 methods, plots)
    ├── data/            # Pre-built RData sample sets (sampleData, CCcolors, EnrichData)
    ├── inst/            # Supplementary assets, extdata, and standalone Shiny scripts
    ├── man/             # Roxygen2 generated Rd documentation files
    ├── vignettes/       # RMarkdown vignettes (foundr.Rmd, foundrShiny.Rmd)
    ├── DESCRIPTION      # Package metadata, version, and dependencies
    └── NAMESPACE        # Exported functions and registered S3 methods

------------------------------------------------------------------------

## 2. Developer Environment & Setup

### System & R Requirements

- **R Version**: `>= 4.2.0`
- **Roxygen2 Version**: `>= 8.0.0`
- **Core Dependencies**: Listed in
  [DESCRIPTION](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/DESCRIPTION)
  (`dplyr`, `tidyr`, `ggplot2`, `broom`, `ordr`, `cowplot`, `ggrepel`,
  `zoo`, `plotly`, `DT`, `purrr`, `tibble`, `rlang`, `readr`, `readxl`).

### Local Development Workflow

To work on `foundr` locally:

``` r

# 1. Open the project in RStudio / Posit Workbench or VS Code

# 2. Install devtools if needed
install.packages("devtools")

# 3. Load package into active session during development
devtools::load_all()

# 4. Generate updated documentation & NAMESPACE
devtools::document()
```

------------------------------------------------------------------------

## 3. Data Model & Founder Strains

### Long-Format Data Model

All primary analysis functions in `foundr` operate on tidy long-format
data frames containing the following standard columns:

| Column | Type | Description |
|----|----|----|
| `dataset` | `character` | Dataset identifier (optional multi-study tag) |
| `strain` | `character` | Founder strain name (one of 8 CC strains) |
| `sex` | `character` | Biological sex (`"M"` / `"F"`) |
| `animal` | `character` | Unique animal or subject identifier |
| `condition` | `character` | Experimental condition or diet treatment (optional) |
| `trait` | `character` | Phenotypic trait name |
| `value` | `numeric` | Measured trait value |

Processed statistical outputs add the following fields: - `signal`:
Fitted strain-sex (-condition) effect estimate - `cellmean`: Total
strain mean (`signal + rest`) - `p.value`: ANOVA F-test p-value for
strain or contrast effect - `SD`: Standard deviation within strain cell

### Collaborative Cross Founder Strains

The 8 Collaborative Cross (CC) founder strains are:  
`AJ`, `B6`, `129`, `NOD`, `NZO`, `CAST`, `PWK`, `WSB`.

Strain color palettes are stored in `CCcolors` (Okabe-Ito color-blind
friendly palette).

------------------------------------------------------------------------

## 4. Core Architecture & S3 Class System

### Data Processing Pipeline

1.  **Orthogonal Variance Partitioning**
    ([R/partition.R](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/partition.R)):  
    [`partition()`](https://byandell-sysgen.github.io/foundr/reference/partition.md)
    decomposes trait values into `signal` (strain x sex x condition),
    `rest` (nuisance/experimental controls), and `noise` (residuals).

2.  **Statistical Summaries & ANOVA**
    ([R/strainstats.R](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/strainstats.R)):  
    [`strainstats()`](https://byandell-sysgen.github.io/foundr/reference/strainstats.md)
    computes linear model parameters, F-statistics, SD, and cell means
    across strain/sex/condition groups.

3.  **Trait Structures (S3 Classes)**:

    - `traitSolos`: Single trait evaluation across strains
    - `traitPairs`: Paired trait relationship analysis (correlations,
      scatter plots)
    - `traitTimes`: Time-series trait trajectories over time
    - `conditionContrasts`: Experimental condition contrast metrics

4.  **S3 Generics & Method Dispatch**: Standard S3 methods implemented
    across trait objects include:  
    [`autoplot()`](https://ggplot2.tidyverse.org/reference/autoplot.html),
    [`plot()`](https://rdrr.io/r/graphics/plot.default.html),
    [`summary()`](https://rdrr.io/r/base/summary.html),
    [`subset()`](https://rdrr.io/r/base/subset.html),
    [`split()`](https://rdrr.io/r/base/split.html),
    [`c()`](https://rdrr.io/r/base/c.html).

5.  **Visualization Design System**: Master ggplot formatting is defined
    in
    [`ggplot_template()`](https://byandell-sysgen.github.io/foundr/reference/ggplot_template.md)
    ([R/ggplot_template.R](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/ggplot_template.R))
    ensuring uniform typography, Okabe-Ito CC color palettes, and
    dynamic faceted layouts. PCA and biplots leverage the `ordr` package
    ([`biplot_signal()`](https://byandell-sysgen.github.io/foundr/reference/biplot_pca.md),
    [`biplot_stat()`](https://byandell-sysgen.github.io/foundr/reference/biplot_pca.md),
    [`biplot_pca()`](https://byandell-sysgen.github.io/foundr/reference/biplot_pca.md)).

------------------------------------------------------------------------

## 5. Development & R Coding Conventions

When writing R code in `foundr`, strictly adhere to these standards:

### Vector Subsetting Safety

When filtering vectors or processing text in R, **always** use explicit
logical indexing with `!grepl(...)` or `grep(..., invert = TRUE)`.

``` r

# CORRECT: Safe logical vector filtering
clean_lines <- lines[!grepl("^\\s*#'", lines)]
clean_lines <- lines[grep("^\\s*#'", lines, invert = TRUE)]

# NEVER USE: !grep(...) evaluates !integer -> FALSE, destroying vectors
# clean_lines <- lines[!grep("^\\s*#'", lines)]  # WRONG
```

### Explicit Package Namespacing

Always use explicit package prefixes (`pkg::func()`) for non-base
functions in exported code to avoid namespace collisions.

``` r

# Example from R/partition.R
object <- dplyr::filter(object, !is.na(.data[[value]]))
fitred <- stats::lm(formred, object)
```

### Explicit Package Imports (No Meta-Packages)

Do not use meta-packages like
[`library(tidyverse)`](https://tidyverse.tidyverse.org) in vignettes,
source functions, or examples. Always import explicit individual
packages ([`library(dplyr)`](https://dplyr.tidyverse.org),
[`library(ggplot2)`](https://ggplot2.tidyverse.org), etc.) to minimize
dependency overhead and prevent build container rendering failures.

### Roxygen2 Documentation

All exported functions in `R/` must include complete Roxygen2 headers: -
Explicit `@param` declarations with expected types - `@return`
descriptions detailing returned structure/S3 class - `@export` tags for
public API functions - `@importFrom` directives for imported utilities -
Executable `@examples` using built-in `sampleData`

------------------------------------------------------------------------

## 6. Testing & Quality Assurance

### Local Verification Commands

Run concrete local verification commands before declaring changes
complete:

``` r
# 1. Update Roxygen2 documentation and NAMESPACE
Rscript -e "devtools::document()"

# 2. Verify interactive loading
Rscript -e "devtools::load_all()"

# 3. Run full package check
Rscript -e "devtools::check(vignettes = FALSE)"
```

------------------------------------------------------------------------

## 7. Version Control & Release Guidelines

### Manual Commit Policy

- **No Automatic Git Operations:** AI assistants and scripts **must
  never** execute `git commit` or `git push`. All staging, committing,
  and pushing are strictly executed manually by the maintainer.

### Release Workflow

1.  Update package version in `DESCRIPTION` (e.g., `1.5.0` -\> `1.5.1`).
2.  Run `devtools::document()` to sync `man/` and `NAMESPACE`.
3.  Run `devtools::check()` to ensure zero errors and zero warnings.
4.  Render vignettes to verify full build cleanliness.
5.  Create version release tag on GitHub.
