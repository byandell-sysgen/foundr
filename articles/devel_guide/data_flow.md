# Data Pipeline & Statistical Methodology

## Data Pipeline & Statistical Methodology

This document details the mathematical models, long-format data schemas,
variance partitioning algorithm, ANCOVA, and longitudinal time-series
handling in `foundr`.

------------------------------------------------------------------------

### 1. Long-Format Data Model

All primary data input objects must be organized in tidy long format
containing:

``` r

# Core input schema:
tibble(
  dataset   = "DietStudy",        # Optional dataset tag
  strain    = "AJ",               # One of 8 CC strains (AJ, B6, 129, NOD, NZO, CAST, PWK, WSB)
  sex       = "F",                # Biological sex ("M" or "F")
  animal    = "1024",             # Subject identifier
  condition = "HF",               # Experimental condition/diet (optional)
  trait     = "Glucose_12wk",     # Trait name
  value     = 142.5               # Measured value
)
```

------------------------------------------------------------------------

### 2. Orthogonal Variance Partitioning

The
[`partition()`](https://byandell-sysgen.github.io/foundr/reference/partition.md)
function
([`R/partition.R`](file:///Users/brianyandell/Documents/Research/byandell-sysgen/foundr/R/partition.R))
separates phenotypic variance into three mutually orthogonal components:

``` math
\text{value} = \text{signal} + \text{rest} + \text{noise}
```

#### Two-Step Linear Model Decomposition

1.  **Reduced Model (Rest Estimation)**: Fit a reduced linear model
    predicting trait value from nuisance/experimental control factors
    ($`\text{rest}`$):
    ``` math
    \text{value} \sim \text{rest}
    ```
    ``` math
    \widehat{\text{rest}} = \text{predict}(\text{fit}_{\text{red}}), \quad e_{\text{red}} = \text{value} - \widehat{\text{rest}}
    ```

2.  **Full Model (Signal Estimation)**: Fit the residuals from the
    reduced model ($`e_{\text{red}}`$) against the signal factors
    ($`\text{signal}`$):
    ``` math
    e_{\text{red}} \sim \text{signal}
    ```
    ``` math
    \widehat{\text{signal}} = \text{predict}(\text{fit}_{\text{full}})
    ```

3.  **Cell Mean Calculation**:
    ``` math
    \text{cellmean} = \widehat{\text{signal}} + \widehat{\text{rest}}
    ```

By default: - When `condition` is present:
`signal = "strain * sex * condition"`,
`rest = "strain * sex + sex * condition"`. - When `condition` is absent:
`signal = "strain * sex"`, `rest = "sex"`.

------------------------------------------------------------------------

### 3. Statistical Summaries & ANCOVA

#### Strain Statistics & ANOVA F-Tests

[`strainstats()`](https://byandell-sysgen.github.io/foundr/reference/strainstats.md)
computes linear models for each trait to evaluate founder strain main
effects and strain-by-sex interactions.

- Cell means: Mean trait value within each `strain x sex x condition`
  cell.
- Cell SDs: Standard deviations computed within each strain cell.
- F-statistics and p-values: Evaluated via
  [`broom::glance()`](https://generics.r-lib.org/reference/glance.html)
  and [`broom::tidy()`](https://generics.r-lib.org/reference/tidy.html).

#### ANCOVA Modeling

[`traitAncova()`](https://byandell-sysgen.github.io/foundr/reference/traitAncova.md)
extends linear modeling by conditioning founder strain effects on
continuous physiological covariates:

``` math
\text{trait} \sim \text{covariate} + \text{strain} \times \text{sex}
```

------------------------------------------------------------------------

### 4. Longitudinal Trait & AUC Integration

For time-series measurements (e.g. weekly body weights or glucose
tolerance test curves), `foundr` provides:

1.  **[`timetraits()`](https://byandell-sysgen.github.io/foundr/reference/timetraits.md)**:
    Parses trait strings containing embedded time suffixes
    (e.g. `Weight_t1`, `Weight_t2`).
2.  **[`area_under_curve()`](https://byandell-sysgen.github.io/foundr/reference/area_under_curve.md)**:
    Computes trapezoidal Area Under the Curve (AUC) over time
    trajectories.
3.  **`traitTimes`**: S3 object wrapping longitudinal trajectories with
    custom
    [`autoplot()`](https://ggplot2.tidyverse.org/reference/autoplot.html)
    methods for visual curve comparisons across founder strains.
