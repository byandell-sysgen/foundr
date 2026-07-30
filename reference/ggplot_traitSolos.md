# GGplot by strain and condition

GGplot by strain and condition

## Usage

``` r
ggplot_traitSolos(object, ...)

# S3 method for class 'traitSolos'
autoplot(object, ...)

# S3 method for class 'traitSolos'
plot(x, ...)
```

## Arguments

- object, x:

  data frame to be plotted

- ...:

  additional parameters (ignored)

- facet_strain:

  facet by strain if \`TRUE\`

- shape_sex:

  use different shape by sex if \`TRUE\`

- boxplot:

  overlay boxplot if \`TRUE\`

- horizontal:

  flip vertical and horizontal axis if \`TRUE\`

## Value

object of class ggplot

## Examples

``` r
ggplot_traitSolos(traitSolos(sampleData))

```
