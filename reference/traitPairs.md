# Prepare pairs of traits for plotting

Prepare pairs of traits for plotting

## Usage

``` r
traitPairs(
  object,
  traitnames = attr(object, "traitnames"),
  pair = paste(traitnames[1:2], collapse = sep),
  sep = " ON ",
  ...
)

# S3 method for class 'traitPairs'
autoplot(object, ...)

# S3 method for class 'traitPairs'
plot(x, ...)
```

## Arguments

- object:

  object of class \`traitSolos\`

- traitnames:

  trait names as \`dataset: trait\`

- pair:

  vector of trait name pairs, each joined by \`sep\`

- sep:

  pair separator

- ...:

  ignored

## Value

object of class \`traitPairs\`

## Examples

``` r
out <- traitSolos(sampleData)
out2 <- traitPairs(out)
plot(out2, parallel_lines = TRUE)
```
