# Volcano Plot

Volcano Plot

## Usage

``` r
volcano(
  object,
  termname = terms[1],
  threshold = threshold_default,
  interact = FALSE,
  traitnames = TRUE,
  facet = FALSE,
  ordername = c("p.value", "kME", "module", "size"),
  xlab = xlab_default,
  ylab = ylab_default,
  ...
)
```

## Arguments

- object:

  data frame from \`strainstats\`

- termname:

  name of \`term\` to show

- threshold:

  named vector for \`SD\` and \`p.value\`

- interact:

  prepare for interactive if \`TRUE\`

- traitnames:

  include trait names if \`TRUE\`

- facet:

  facet on \`strain\` if \`TRUE\`

- ordername:

  name of column for Y ordering.

- xlab, ylab:

  axis labels

- ...:

  additional parameters ignored

## Value

ggplot object

## Examples

``` r
sampleStats <- strainstats(sampleData)
volcano(sampleStats)
#> Warning: Removed 1 row containing missing values or values outside the scale range
#> (`geom_text_repel()`).
```
