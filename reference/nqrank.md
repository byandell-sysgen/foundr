# Normal scores as qnorm of rank

Copied from github.com/kbroman/broman package

## Usage

``` r
nqrank(x, jitter = FALSE, standard = FALSE)
```

## Arguments

- x:

  vector of measurements

- jitter:

  jitter values slightly if \`TRUE\`

- standard:

  standardize to mean 0, variance 1 if \`TRUE\`

## Value

vector of normal scores

## Examples

``` r
nqrank(1:10)
#>  [1]  0.4630762  2.3262003  3.4345558  4.3200593  5.1151958  5.8848042
#>  [7]  6.6799407  7.5654442  8.6737997 10.5369238
```
