# Prepare biplot signal data

Prepare biplot signal data

Prepare biplot stats

Get PCA components from biplot data

Biplot using ggplot2 via ordr package

BiPlot for Evidence vs Spread

## Usage

``` r
biplot_signal(
  object,
  datatraits = unique(object$datatrait),
  orders = c("module", "kME", "p.value", "size")
)

biplot_stat(object, datatraits = unique(object$datatrait), orders = terms)

biplot_pca(
  bip,
  size = c("module", "kME", "p.value", "size"),
  strain = "NONE",
  threshold
)

biggplot(bip_pca, axes = 1:2, scale.factor = 2)

biplot_evidence(
  object,
  ordername,
  xlab,
  threshold,
  strain = "NONE",
  axes = 1:2,
  ...
)
```

## Arguments

- object:

  data frame

- datatraits:

  \`dataset: trait\` names to include

- orders:

  column names used for ordering and plot sizes

- bip:

  object from \`biplot_signal\`

- strain:

  strain name to highlight in biplot

- threshold:

  vector of threshold values

- bip_pca:

  object of class bip_pca

- axes:

  axes to plot

- scale.factor:

  scale factor for arrows vs points

- ordername:

  name of order column

- xlab:

  x label

- ...:

  additional paramaters ignored

- transpose:

  transpose for \`princomp\` if \`TRUE\`

## Value

data frame

data frame

data frame of PCA components

object of class ggplot2

gg plot object
