# GGplot of WGCNA Modules

GGplot of WGCNA Modules

Autoplot of wgcnaModules

GGplot of List of WGCNA Modules

Autoplot of wgcnaModules

## Usage

``` r
ggplot_wgcnaModules(
  object,
  response = names(object),
  main = paste("Dendrogram for", response, "with module colors"),
  ...
)

# S3 method for class 'wgcnaModules'
autoplot(object, ...)

ggplot_listof_wgcnaModules(
  object,
  response = names(object),
  main = paste("Dendrogram for", response, "with module colors"),
  ...
)

# S3 method for class 'listof_wgcnaModules'
autoplot(object, ...)
```

## Arguments

- object:

  object of class `listof_wgcnaModules`

- response:

  response for dendrogram and primary color band

- main:

  title of plot

- ...:

  additional parameters

## Value

ggplot2 object

ggplot2 object

ggplot2 object

ggplot2 object
