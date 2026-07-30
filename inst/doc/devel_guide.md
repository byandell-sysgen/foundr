# Creating the foundr Developer Guide

This document records the step-by-step process, prompts, blueprint references, design decisions, and build/deployment procedures used to create the `foundr` developer guide vignette suite (`vignettes/devel_guide/`), root `DEVELOPER.md`, and `pkgdown` website configuration.

---

## 1. User Prompt & Blueprint Context

### Original User Prompts

**Prompts:**

- Create a `DEVELOPER.md` file for this project
- Following `../foundrShiny/inst/doc/devel_guide.md` create a Developer Guide and document in `inst/doc/devel_guide.md`

### Reference Blueprints Used

1. **`../foundrShiny/inst/doc/devel_guide.md`**:
   - Outlined master index structure (`vignettes/devel_guide/index.Rmd`), sub-module guides, layout conventions, `.nojekyll` setup, and `pkgdown` article integration.
2. **`~/Documents/GitHub/Documentation/github/pkgdown.md`**:
   - Outlined `_pkgdown.yml` configuration, article grouping rules (including quoting subdirectory paths like `"devel_guide/index"`), `.Rbuildignore` anchored exclusions, `.nojekyll` creation, and `mermaid.js` script header injection (`template.includes.in_header`).
3. **`~/Documents/GitHub/Documentation/prompts/devel_guide.md`**:
   - Provided layout conventions, code chunk tagging, and multi-part article hierarchy.

---

## 2. Process & Step-by-Step Implementation

### Step 1: Root Reference File (`DEVELOPER.md`)

Created [`DEVELOPER.md`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/DEVELOPER.md) in the project root detailing package architecture, data models, developer environment setup, R coding conventions, S3 object patterns, testing procedures, and release workflows.

### Step 2: Architectural Analysis of `foundr`

Inspected `R/*.R` source files and `AGENTS.md` to map out core statistical algorithms, variance partitioning logic (`partition()`), S3 trait class dispatches (`traitSolos`, `traitPairs`, `traitTimes`, `conditionContrasts`), visualization templates (`ggplot_template()`), and `ordr`-backed biplot implementations.

### Step 3: Creation of `vignettes/devel_guide/` Suite

Created a 3-part R Markdown article suite under `vignettes/devel_guide/`:

- **[`vignettes/devel_guide/index.Rmd`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/vignettes/devel_guide/index.Rmd)**:
  - Master index article providing package purpose, companion package mapping (`foundrShiny`, `foundrHarmony`, `modulr`), local developer quick start commands, and a full visual `mermaid` flowchart mapping data input -> variance partitioning (`partition()`) -> statistical summaries (`strainstats()`) -> S3 trait object construction -> `autoplot()` / `ggplot_*()` / `biplot_*()` visualization layers.
- **[`vignettes/devel_guide/modules.Rmd`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/vignettes/devel_guide/modules.Rmd)**:
  - Exhaustive 5-category breakdown of package functions, S3 classes, generics, WGCNA module integrations, visualization engines, and data transformation utilities.
- **[`vignettes/devel_guide/data_flow.Rmd`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/vignettes/devel_guide/data_flow.Rmd)**:
  - Technical specification of long-format data schemas, linear model equations for orthogonal variance partitioning ($\text{value} = \text{signal} + \text{rest} + \text{noise}$), ANCOVA modeling, and time-series trapezoidal AUC calculations.

### Step 4: `_pkgdown.yml` & Mermaid.js Integration

Created [`_pkgdown.yml`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/_pkgdown.yml) in package root:

- Configured Bootstrap 5 theme.
- Added Mermaid.js CDN script injection in `template.includes.in_header` to automatically render `mermaid` flowcharts on `pkgdown` site pages.
- Grouped developer articles under `"devel_guide/index"`, `"devel_guide/modules"`, and `"devel_guide/data_flow"`.

### Step 5: `.Rbuildignore` & `.nojekyll` Setup

- Updated [`.Rbuildignore`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/.Rbuildignore) with anchored regex exclusions (`^_pkgdown\.yml$`, `^\.github$`, `^docs$`).
- Created [`docs/.nojekyll`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/docs/.nojekyll) to ensure GitHub Pages does not ignore underscore asset folders (`_pkgdown.yml`, `_site`, `_deps`).

---

## 3. GitHub Pages & Website Publishing

When `pkgdown::build_site()` runs, it compiles static HTML files into `docs/`:

- **Main Developer Guide & Mermaid Flowchart**: `articles/devel_guide/index.html`
- **Function Index & S3 System**: `articles/devel_guide/modules.html`
- **Data Pipeline & Methodology**: `articles/devel_guide/data_flow.html`
- **Articles Landing Page**: `articles/index.html`

### GitHub Pages Configuration

To serve the site from the `main` branch when `pkgdown` builds into `docs/`:

1. In GitHub Repository Settings -> **Pages**.
2. Set **Branch**: `main` and **Folder**: `/docs`.

---

## 4. Verification Commands

The developer guide suite and package site can be built and verified locally:

```r
# Generate documentation and NAMESPACE
devtools::document()

# Compile vignettes / pkgdown articles
pkgdown::build_articles()

# Build full pkgdown site into docs/
pkgdown::build_site(install = FALSE)

# Package check
devtools::check(cran = FALSE, vignettes = FALSE)
```
