# Extreme correlation comparison summaries

Extreme correlation comparison summaries

## Usage

``` r
cor_extreme(
  traitStats,
  object = cor_compare(traitStats, ...),
  ...,
  cormin = 0.8,
  minlogp = 2
)
```

## Arguments

- traitStats:

  data frame with trait summaries

- object:

  object from \`cor_compare()\`

- ...:

  additional parameters

- cormin:

  minimum correlation to keep

- minlogp:

  minimul log of p-value to keep

## Value

data frame
