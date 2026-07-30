# Function Index & S3 Class System Breakdown

## Function Index & S3 Class System Breakdown

`foundr` organizes its source code across 45+ source files in `R/`.
Functions are grouped into five core architectural categories:

------------------------------------------------------------------------

### 1. Data Analysis & Statistical Modeling

| Function | Primary Role / Description | Source File |
|----|----|----|
| [`partition()`](https://byandell-sysgen.github.io/foundr/reference/partition.md) | Decomposes raw trait values into orthogonal `signal`, `rest`, and `noise` terms | [`R/partition.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/partition.R) |
| [`strainstats()`](https://byandell-sysgen.github.io/foundr/reference/strainstats.md) | Computes strain/sex/condition summary stats, standard deviations, cell means, and ANOVA F-tests | [`R/strainstats.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/strainstats.R) |
| [`conditionContrasts()`](https://byandell-sysgen.github.io/foundr/reference/conditionContrasts.md) | Calculates differences and contrasts between experimental conditions across founder strains | [`R/conditionContrasts.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/conditionContrasts.R) |
| [`bestcor()`](https://byandell-sysgen.github.io/foundr/reference/bestcor.md) | Identifies top correlated traits across founder strains using Spearman rank correlation | [`R/bestcor.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/bestcor.R) |
| [`eigen_cor()`](https://byandell-sysgen.github.io/foundr/reference/eigen_cor.md) / [`eigen_contrast()`](https://byandell-sysgen.github.io/foundr/reference/eigen_contrast.md) | Computes eigentrait correlations and condition contrast eigentrait projections | [`R/eigentrait.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/eigentrait.R) |
| [`traitAncova()`](https://byandell-sysgen.github.io/foundr/reference/traitAncova.md) | Performs Analysis of Covariance (ANCOVA) combining continuous covariates and strain factors | [`R/traitAncova.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/traitAncova.R) |

------------------------------------------------------------------------

### 2. Trait S3 Class System & Method Dispatch

`foundr` implements custom S3 classes to encapsulate structured trait
data and provide unified visualization & summary APIs.

#### S3 Classes

- **`traitSolos`**: Represents single-trait data structured for strain
  comparisons
  ([`R/traitSolos.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/traitSolos.R)).
- **`traitPairs`**: Encapsulates bivariate trait comparisons, joint
  distributions, and correlations
  ([`R/traitPairs.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/traitPairs.R)).
- **`traitTimes`**: Wraps time-series measurement trajectories over time
  points
  ([`R/traitTimes.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/traitTimes.R)).
- **`conditionContrasts`**: Encapsulates condition contrast effect
  estimates and p-values
  ([`R/conditionContrasts.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/conditionContrasts.R)).

#### Standardized S3 Generics

Each S3 trait class supports standard S3 generics: -
[`autoplot()`](https://ggplot2.tidyverse.org/reference/autoplot.html) /
[`plot()`](https://rdrr.io/r/graphics/plot.default.html): Generate
`ggplot2` visual representations. -
[`summary()`](https://rdrr.io/r/base/summary.html): Produce numerical
summaries and strain contrast tables. -
[`subset()`](https://rdrr.io/r/base/subset.html) /
[`split()`](https://rdrr.io/r/base/split.html) /
[`c()`](https://rdrr.io/r/base/c.html): Manipulate, slice, or combine
trait objects seamlessly.

------------------------------------------------------------------------

### 3. Module Analysis & WGCNA Integration

`foundr` integrates with WGCNA module outputs to analyze co-expression
gene modules alongside physiological phenotypes:

- [`module_kMEs()`](https://byandell-sysgen.github.io/foundr/reference/module_kMEs.md):
  Extracts module eigengene kME values for specified traits
  ([`R/module_kMEs.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/module_kMEs.R)).
- [`module_band()`](https://byandell-sysgen.github.io/foundr/reference/module_band.md):
  Computes module band intervals across founder strain trait signals
  ([`R/module_band.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/module_band.R)).
- `wgcnaModules()` / `listof_wgcnaModules()`: Constructors for managing
  single and list-of-WGCNA module specifications
  ([`R/wgcnaModules.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/wgcnaModules.R)).

------------------------------------------------------------------------

### 4. Visualization & Biplot Engine

All plot generators in `foundr` build upon the centralized
[`ggplot_template()`](https://byandell-sysgen.github.io/foundr/reference/ggplot_template.md)
design system:

| Plot Function | Description | Source File |
|----|----|----|
| [`ggplot_template()`](https://byandell-sysgen.github.io/foundr/reference/ggplot_template.md) | Core styling template (Okabe-Ito CC color palette, custom themes, facet options) | [`R/ggplot_template.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/ggplot_template.R) |
| [`ggplot_traitSolos()`](https://byandell-sysgen.github.io/foundr/reference/ggplot_traitSolos.md) | Bar charts and point plots for single trait strain values | [`R/traitSolos.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/traitSolos.R) |
| [`ggplot_traitPairs()`](https://byandell-sysgen.github.io/foundr/reference/ggplot_traitPairs.md) | Scatter plots and correlation grids for paired traits | [`R/traitPairs.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/traitPairs.R) |
| [`ggplot_traitTimes()`](https://byandell-sysgen.github.io/foundr/reference/traitTimes.md) | Longitudinal trajectory plots across experimental time points | [`R/traitTimes.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/traitTimes.R) |
| [`volcano()`](https://byandell-sysgen.github.io/foundr/reference/volcano.md) | Volcano plots mapping effect size against statistical significance ($`-\log_{10}(p)`$) | [`R/volcano.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/volcano.R) |
| [`biplot_signal()`](https://byandell-sysgen.github.io/foundr/reference/biplot_pca.md) / [`biplot_pca()`](https://byandell-sysgen.github.io/foundr/reference/biplot_pca.md) | PCA biplot visualizations powered by the `ordr` package | [`R/biplot.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/biplot.R) |
| [`ggplot_evidence_spread()`](https://byandell-sysgen.github.io/foundr/reference/ggplot_evidence_spread.md) | Evidence spread and rank variance dot plots | [`R/evidence_spread.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/evidence_spread.R) |

------------------------------------------------------------------------

### 5. Utilities & Data Transformation Helpers

- [`nqrank()`](https://byandell-sysgen.github.io/foundr/reference/nqrank.md)
  / `normalscores()`: Normal quantile rank transformations for
  non-Gaussian trait normalization
  ([`R/nqrank.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/nqrank.R)).
- [`area_under_curve()`](https://byandell-sysgen.github.io/foundr/reference/area_under_curve.md):
  Integrates trait values across longitudinal time points
  ([`R/area_under_curve.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/area_under_curve.R)).
- [`unite_datatraits()`](https://byandell-sysgen.github.io/foundr/reference/unite_datatraits.md)
  /
  [`pivot_pair()`](https://byandell-sysgen.github.io/foundr/reference/pivot_pair.md):
  Reshaping helpers for combining dataset names and trait identifiers
  ([`R/trait_names.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/trait_names.R)).
- [`timetraits()`](https://byandell-sysgen.github.io/foundr/reference/timetraits.md)
  /
  [`separate_time()`](https://byandell-sysgen.github.io/foundr/reference/separate_time.md):
  Utilities for parsing time component tags from trait string names
  ([`R/timetraits.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/timetraits.R)).
