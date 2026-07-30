# Calculate Absolute Correlations

Calculate Absolute Correlations

## Usage

``` r
abscorcalc(object, method = c("spearman", "pearson"), abs = TRUE)
```

## Arguments

- object:

  data frame

- method:

  method for correlation

- abs:

  absolute correlation if \`TRUE\`

## Value

data frame with design columns, \`trait\` names and \`value\` of
absolute correlations

## Examples

``` r
abscorcalc(sampleData)
#>            C          A          D          B
#> C 1.00000000 0.01900042 0.06395133 0.06123725
#> A 0.01900042 1.00000000 0.15577688 0.07198552
#> D 0.06395133 0.15577688 1.00000000 0.39671354
#> B 0.06123725 0.07198552 0.39671354 1.00000000
```
