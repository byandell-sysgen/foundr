# GGplot of evidence vs spread

This includes volcano plot and other plots that compare data spread to
strength of evidence. The strength of evidence is often a \`p.value\`
(typically plotted as \`-log10(p.value)\`) but need not be. The spread
may be differences of mean values or SDs (square root of MS for model
term).

## Usage

``` r
ggplot_evidence_spread(
  object,
  xlab = NULL,
  plottype = c("dotplot", "volcano", "biplot"),
  ordername = attr(object, "ordername"),
  ntrait = 20,
  ...
)
```

## Arguments

- object:

  data frame with optional attributes

- xlab:

  replacement horizontal label if not \`NULL\`

- plottype:

  type of plot

- ordername:

  column name to order entries

- ntrait:

  number of traits to plot

- ...:

  additional parameters ignored

## Value

GG plot object
