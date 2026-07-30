# Trait Analysis of Covariance

Trait Analysis of Covariance

Summary of Trait Ancova

GGplot of Trait Ancova

## Usage

``` r
traitAncova(
  traitData,
  traitStats,
  covarData,
  focus = c("Driver", "Target"),
  trait_name,
  condition_name = "diet"
)

summary_traitAncova(traitAncova, traits = NULL)

ggplot_traitAncova(
  traitAncova,
  traits = NULL,
  signif_level = 0.05,
  width = 0.1,
  height = 0
)
```

## Arguments

- traitData:

  data frame of trait data

- traitStats:

  data frame of trait stats

- covarData:

  data frame of covariate data

- focus:

  focus of mediation

- trait_name:

  character string of focal trait name

- condition_name:

  character string of condition name

- traitAncova:

  object of class \`traitAncova\`

- traits:

  trait names to give unique colors

- signif_level:

  significance level

- width, height:

  jitter offsets

## Value

object of class \`traitAncova\`

data frame as summary

ggplot object
