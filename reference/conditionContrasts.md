# Contrasts of Conditions

Contrasts of Conditions

GGplot of Contrasts of Conditions

Plot method for Contrasts of Conditions

Summary method for Contrasts of Condtions

Summary method for Contrasts of Conditions

Combine method for Contrasts of Conditions

Split method for Contrasts of Conditions

## Usage

``` r
conditionContrasts(
  traitSignal,
  traitStats,
  termname = "signal",
  rawStats = traitStats
)

ggplot_conditionContrasts(
  object,
  bysex = c("Both Sexes", "Female", "Male", "Sex Contrast"),
  ...
)

# S3 method for class 'conditionContrasts'
plot(x, ...)

summary_conditionContrasts(
  object,
  ntrait = 0,
  sortby = ordername,
  ordername = attr(object, "ordername"),
  ...
)

# S3 method for class 'conditionContrasts'
summary(object, ...)

# S3 method for class 'conditionContrasts'
c(...)

# S3 method for class 'conditionContrasts'
split(x, ...)
```

## Arguments

- traitSignal:

  data frame of signals

- traitStats:

  data frame of stats

- termname:

  name of term

- rawStats:

  data frame with \`rawSD\`

- object:

  object of class \`conditionContrasts\`

- bysex:

  type of sex from c("F","M","F-M","F+M")

- ...:

  additional parameters for generic \`split\`

- x:

  objects of class \`conditionContrasts\`

- ntrait:

  number of traits to plot

- sortby:

  sort summary by this variable

- ordername:

  column name to order entries

## Value

object of class \`conditionContrasts\`

ggplot object

ggplot object

data frame

data frame

object of class \`conditionContrasts\`

object of class \`conditionContrasts\`
