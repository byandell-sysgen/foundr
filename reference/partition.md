# Partition Trait into Signal, Rest and Noise

Partition a trait value into three parts based on rest and signal
factors. The signal is the main interest for comparison across traits,
while the rest concerns aspects of the experiment that are controlled.
Noise is unexplained variation. The three parts will be orthogonal to
each other. The \`signal\` factors, entered as terms for \`formula\`,
are conditioned by the \`rest\` factors.

## Usage

``` r
partition(
  object,
  trait = "trait",
  value = "value",
  signal = ifelse(is_condition, "strain * sex * condition", "strain * sex"),
  rest = ifelse(is_condition, "strain * sex + sex * condition", "sex")
)
```

## Arguments

- object:

  data frame in long format with trait data

- trait:

  name of column with trait names

- value:

  name column with trait values

- signal:

  signal factor combination as string for \`formula\`

- rest:

  rest factor combination as string for \`formula\`

## Value

data frame with added columns \`signal\`, \`cellmean\`

## Examples

``` r
partition(sampleData)
#> # A tibble: 128 × 7
#>    dataset trait strain sex   condition  signal cellmean
#>    <chr>   <fct> <chr>  <chr> <chr>       <dbl>    <dbl>
#>  1 sample  C     B6     F     Y          0.311    0.599 
#>  2 sample  C     B6     F     X         -0.414   -0.0951
#>  3 sample  C     B6     M     X         -0.429   -1.62  
#>  4 sample  C     B6     M     Y          0.286   -1.00  
#>  5 sample  C     129    M     X         -0.0601  -0.648 
#>  6 sample  C     129    F     X          0.0751  -0.307 
#>  7 sample  C     129    F     Y         -0.0751  -0.487 
#>  8 sample  C     129    M     Y          0.0601  -0.626 
#>  9 sample  C     AJ     F     X          0.445    1.67  
#> 10 sample  C     AJ     F     Y         -0.445    0.752 
#> # ℹ 118 more rows
```
