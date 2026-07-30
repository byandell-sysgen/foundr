# Stats over Time

Stats over Time

## Usage

``` r
stats_time(
  traitStats,
  traitnames = timetraits(traitStats, timecol)[1],
  response = c("p.value", "SD"),
  timecol = c("week", "minute", "minute_summary", "week_summary"),
  models = c("terms", "parts"),
  ...
)
```

## Arguments

- traitStats:

  data frame with trait stats from \`strainstats\`

- traitnames:

  names of \`dataset: trait\`

- response:

  character string for type of response

- timecol:

  column to use for time

- models:

  parts of model to include

- ...:

  additional parameters ignored
