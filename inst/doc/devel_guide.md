# Creating the foundr Developer Guide

This document records the step-by-step process, prompts, blueprint references, and design decisions used to create the `foundr` developer guide vignette suite (`vignettes/devel_guide/`) and `pkgdown` website configuration.

---

## 1. User Prompt & Blueprint Context

### Original User Prompt

Following `../foundrShiny/inst/doc/devel_guide.md` create a Developer Guide and document in `inst/doc/devel_guide.md`.

### Reference Blueprints Used

1. **`../foundrShiny/inst/doc/devel_guide.md`**:
   - Outlined master index structure (`vignettes/devel_guide/index.Rmd`), sub-module/function guides, data flow specifications, and `pkgdown` article integration.
2. **`~/Documents/GitHub/Documentation/github/pkgdown.md`**:
   - Outlined `_pkgdown.yml` configuration, article grouping rules (quoting subdirectory paths like `"devel_guide/index"`), `.Rbuildignore` anchored exclusions, and `mermaid.js` script header injection (`template.includes.in_header`).
3. **`~/Documents/GitHub/Documentation/prompts/devel_guide.md`**:
   - Provided layout conventions, code chunk tagging, and multi-part article hierarchy.

---

## 2. Process & Step-by-Step Implementation

### Step 1: Architectural Analysis of `foundr`

Inspected `R/*.R` source files and `AGENTS.md` to map out the core statistical algorithms, variance partitioning logic, S3 trait class dispatches (`traitSolos`, `traitPairs`, `traitTimes`, `conditionContrasts`), visualization templates (`ggplot_template()`), and `ordr`-backed biplot implementations.

### Step 2: Creation of `vignettes/devel_guide/` Suite

Created a 3-part R Markdown article suite under `vignettes/devel_guide/`:

- **[`vignettes/devel_guide/index.Rmd`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/vignettes/devel_guide/index.Rmd)**:
  - Master index article providing package purpose, companion package mapping (`foundrShiny`, `foundrHarmony`, `modulr`), local developer quick start commands, and a full visual `mermaid` flowchart mapping data input -> variance partitioning (`partition()`) -> statistical summaries (`strainstats()`) -> S3 trait object construction -> `autoplot()` / `ggplot_*()` / `biplot_*()` visualization layers.
- **[`vignettes/devel_guide/modules.Rmd`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/vignettes/devel_guide/modules.Rmd)**:
  - Exhaustive 5-category breakdown of package functions, S3 classes, generics, WGCNA module integrations, visualization engines, and data transformation utilities.
- **[`vignettes/devel_guide/data_flow.Rmd`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/vignettes/devel_guide/data_flow.Rmd)**:
  - Technical specification of long-format data schemas, linear model equations for orthogonal variance partitioning ($\text{value} = \text{signal} + \text{rest} + \text{noise}$), ANCOVA modeling, and time-series trapezoidal AUC calculations.

### Step 3: `_pkgdown.yml` & Mermaid.js Integration

Created `_pkgdown.yml` in the package root:

- Configured Bootstrap 5 theme.
- Added Mermaid.js CDN script injection in `template.includes.in_header` to automatically render `mermaid` flowcharts on `pkgdown` site pages.
- Grouped developer articles under `"devel_guide/index"`, `"devel_guide/modules"`, and `"devel_guide/data_flow"`.

### Step 4: `.Rbuildignore` & Build Exclusion Hygiene

Updated `.Rbuildignore` with anchored regex exclusions:

```regex
^.*\.Rproj$
^\.Rproj\.user$
rsconnect/
inst/shinyApp/rsconnect
^foundr\.Rproj$
^_pkgdown\.yml$
^\.github$
^docs$
```

---

## 3. Verification Commands

The developer guide suite can be compiled and verified using standard R developer tools:

```r
# Build vignettes
devtools::build_vignettes()

# Build full pkgdown site
pkgdown::build_site_github_pages(new_process = FALSE, install = FALSE)

# Package check
devtools::check(cran = FALSE, vignettes = FALSE)
```
