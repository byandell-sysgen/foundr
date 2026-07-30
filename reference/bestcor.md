# Traits with Best Correlation

Find other traits with best Spearman correlation with selected
traitnames.

## Usage

``` r
bestcor(traitSignal, traitnames = NULL, term = c("cellmean", "signal"))

is_bestcor(object)

ggplot_bestcor(object, mincor = 0.7, abscor = TRUE, ...)

# S3 method for class 'bestcor'
autoplot(object, ...)

summary_bestcor(object, mincor = 0.5, ...)

# S3 method for class 'bestcor'
summary(object, ...)
```

## Arguments

- traitSignal:

  data frame from \`partition\`

- traitnames:

  names of traits in \`traitSignal\`

- term:

  either \`signal\` or \`mean\`

- object:

  object of class \`bestcor\`

- mincor:

  minimum correlation to show

- abscor:

  plot absolute value of correlation if \`TRUE\`

- ...:

  not used

## Value

sorted vector of absolute correlations with names

logical

ggplot object

data frame

## Examples

``` r
sampleSignal <- partition(sampleData)
out <- bestcor(sampleSignal, "sample: A")
ggplot_bestcor(out, 0)

ggplot_bestcor(out, 0, abscor = FALSE)
```
