# Correlation of eigentraits across responses

Correlation of eigentraits across responses

GGplot of Eigentrait Correlations

## Usage

``` r
eigen_cor(object)

ggplot_eigen_cor(
  object,
  facetname,
  colorname,
  main = paste("facet by", facetname, "with", colorname, "color"),
  ...
)

# S3 method for class 'eigen_cor'
autoplot(object, ...)

# S3 method for class 'eigen_cor'
subset(x, ...)
```

## Arguments

- object:

  object with \`eigen\` element

- facetname:

  facet name

- colorname:

  color name

- main:

  title

- ...:

  additional parameters

- object, x:

  object of class \`eigen_cor\`

## Value

data frame of class \`eigen_cor\`

ggplot object
