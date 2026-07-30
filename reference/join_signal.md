# Join trait data and signal

Join trait data and signal

## Usage

``` r
join_signal(traitData, traitSignal, response = c("rest", "noise"))
```

## Arguments

- traitData:

  data frame with harmonized data

- traitSignal:

  data frame with \`signal\` and \`cellmean\`

- response:

  name of response to create through joining

## Value

data frame with \`value\` as \`rest\` or \`noise\` column
