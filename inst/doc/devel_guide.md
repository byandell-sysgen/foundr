# Creating the foundr Developer Guide

This document records the step-by-step process, prompts, blueprint references, design decisions, and build/deployment procedures used to create the `foundr` developer guide vignette suite (`vignettes/devel_guide/`), root `DEVELOPER.md`, and `pkgdown` website configuration.

---

## 1. User Prompt & Blueprint Context

### Original User Prompts

**Prompts:**

- Create a `DEVELOPER.md` file for this project
- Following `../foundrShiny/inst/doc/devel_guide.md` create a Developer Guide and document in `inst/doc/devel_guide.md`
- I have changed GitHub Pages back to root (/). Please reread `../foundrShiny/inst/doc/devel_guide.md` and make changes to pkgdown or other files to match.
- Action error refers to tidyverse. We should not be using tidyverse (a huge meta-package) but rather explicit packages.
- The `vignettes/foundrShiny.Rmd` is out of date and should be in `../foundrShiny/vignettes`. Place it there and I will update when working on that project. The developer guide listing in `_pkgdown.yml` should have its subpages (modules, data_flow) indented.

### Reference Blueprints Used

1. **`../foundrShiny/inst/doc/devel_guide.md`**:
   - Outlined master index structure (`vignettes/devel_guide/index.Rmd`), sub-module guides, layout conventions, `.nojekyll` setup, GitHub Actions CI/CD deployment (`.github/workflows/pkgdown.yaml`), and `pkgdown` article integration.
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

### Step 3: Creation of `vignettes/devel_guide/` Suite & Vignette Hygiene

Created a 3-part R Markdown article suite under `vignettes/devel_guide/`:

- **[`vignettes/devel_guide/index.Rmd`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/vignettes/devel_guide/index.Rmd)**:
  - Master index article providing package purpose, companion package mapping (`foundrShiny`, `foundrHarmony`, `modulr`), local developer quick start commands, and a full visual `mermaid` flowchart mapping data input -> variance partitioning (`partition()`) -> statistical summaries (`strainstats()`) -> S3 trait object construction -> `autoplot()` / `ggplot_*()` / `biplot_*()` visualization layers.
- **[`vignettes/devel_guide/modules.Rmd`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/vignettes/devel_guide/modules.Rmd)**:
  - Exhaustive 5-category breakdown of package functions, S3 classes, generics, WGCNA module integrations, visualization engines, and data transformation utilities.
- **[`vignettes/devel_guide/data_flow.Rmd`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/vignettes/devel_guide/data_flow.Rmd)**:
  - Technical specification of long-format data schemas, linear model equations for orthogonal variance partitioning ($\text{value} = \text{signal} + \text{rest} + \text{noise}$), ANCOVA modeling, and time-series trapezoidal AUC calculations.
- **[`vignettes/foundr.Rmd`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/vignettes/foundr.Rmd)**:
  - Updated vignette imports to use explicit packages (`library(dplyr)`, `library(ggplot2)`) instead of the `tidyverse` meta-package to ensure clean rendering in automated build containers.
- **Relocation of `foundrShiny.Rmd`**:
  - Moved out-of-date `vignettes/foundrShiny.Rmd` to `../foundrShiny/vignettes/foundrShiny.Rmd` to be maintained within the `foundrShiny` workspace.

### Step 4: `_pkgdown.yml` & Navigation Design

Updated [`_pkgdown.yml`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/_pkgdown.yml) in package root:

- Configured Bootstrap 5 theme with Mermaid.js CDN script injection in `template.includes.in_header`.
- Set top navigation dropdown component to `text: Guides` matching `qtl2shiny`.
- Indented developer guide subpages (`modules`, `data_flow`) under the master index in the navbar menu dropdown.
- Grouped articles under `User Guides` (`"foundr"`) and `Developer Guides` (`"devel_guide/index"`, `"devel_guide/modules"`, `"devel_guide/data_flow"`).

### Step 5: Build Exclusion Hygiene & CI/CD Setup

- Updated [`.Rbuildignore`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/.Rbuildignore) with anchored regex exclusions (`^_pkgdown\.yml$`, `^\.github$`, `^docs$`).
- Updated [`.gitignore`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/.gitignore) to ignore `docs/` so local builds keep `main` clean.
- Created [`.github/workflows/pkgdown.yaml`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/.github/workflows/pkgdown.yaml) using `JamesIves/github-pages-deploy-action@v4` for automated GitHub Actions deployment to the `gh-pages` branch.

---

## 3. GitHub Pages Automated CI/CD Publishing via `gh-pages`

To avoid cluttering the `main` branch git history with hundreds of compiled HTML files from `docs/`:

1. **Keep `docs/` in `.gitignore`**: Local `pkgdown::build_site()` builds remain untracked in your local workspace, keeping `main` clean (source files only).
2. **Automated Deployment via [.github/workflows/pkgdown.yaml](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/.github/workflows/pkgdown.yaml)**:
   - On every `git push` to `main`, GitHub Actions runs `pkgdown::build_site()` in a cloud container.
   - The workflow step `JamesIves/github-pages-deploy-action@v4` commits the compiled site directly to an isolated, automated **`gh-pages`** branch.
3. **GitHub Pages Setting**:
   - On GitHub.com under **Settings** -> **Pages**:
     - Set **Source**: **Deploy from a branch**
     - Set **Branch**: **`gh-pages`** / **`/ (root)`**
     - Click **Save**

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
