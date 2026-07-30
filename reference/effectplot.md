# Effect Plots

Effect Plots

## Usage

``` r
effectplot(object, traitnames = NULL, correlated = NULL, ...)
```

## Arguments

- object:

  data frame from \`strainstats()\`

- traitnames:

  \`traitnames\` to show

- correlated:

  correlated \`traitnames\` to overlay on boxplot (optional)

- ...:

  additional parameters

## Value

ggplot object

## Examples

``` r
sampleStats <- strainstats(sampleData)
effectplot(sampleStats, trait_names(sampleStats, "C"))

```
