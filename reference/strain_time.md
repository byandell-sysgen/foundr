# Strains over Time

Strains over Time

## Usage

``` r
strain_time(
  traitData,
  traitSignal,
  traitnames = timetraits(traitSignal, timecol)[1],
  timecol = c("week", "minute", "minute_summary", "week_summary"),
  response = c("value", "normed", "cellmean", "signal"),
  strains = names(foundr::CCcolors),
  ...
)
```

## Arguments

- traitData:

  data frame with trait data

- traitSignal:

  data from with trait signals

- traitnames:

  names of \`dataset: trait\` without \`timecol\` information

- timecol:

  column to use for time

- response:

  character string for type of response

- strains:

  names of strains to subset

- ...:

  additional parameters ignored
