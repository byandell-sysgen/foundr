# Traits over Time

Traits over Time

GGplot of Strains over Time

## Usage

``` r
traitTimes(traitData, traitSignal, traitStats, ...)

ggplot_traitTimes(
  object,
  objectSum = NULL,
  ...,
  drop_xlab = TRUE,
  facet_strain = (timetype != "strain"),
  legend_position = "bottom"
)

# S3 method for class 'traitTimes'
autoplot(object, ...)

# S3 method for class 'traitTimes'
plot(x, ...)
```

## Arguments

- traitSignal:

  data from with trait signals

- ...:

  additional parameters

- object:

  data frame with trait data or trait stats from \`strainstats\`

- drop_xlab:

  drop xlab for all but last plot if \`TRUE\`

- legend_position:

  position of legend ("none" for none)

- traitnames:

  names of \`dataset: trait\`

- response:

  character string for type of response

- timecol:

  column to use for time

- object, objectSum:

  object of class \`strain_time\`

## Value

object of class \`traitTimes\`

ggplot object
