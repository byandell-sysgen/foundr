# Extract Modules and kMEs

Extract Modules and kMEs

GGplot of Module kMEs

Subset module and kMEs

## Usage

``` r
module_kMEs(object)

ggplot_module_kMEs(
  object,
  facetname,
  colorname,
  abskME = FALSE,
  title = paste("facet by", facetname, "with", colorname, "color"),
  ...
)

# S3 method for class 'module_kMEs'
autoplot(object, ...)

subset_module_kMEs(
  x,
  facetname,
  colorname,
  facetmodules = flev,
  colormodules = clev,
  ...
)

# S3 method for class 'module_kMEs'
subset(x, ...)
```

## Arguments

- object:

  object of class \`module_kMEs\`

- facetname:

  name of facet response

- colorname:

  name of color response

- abskME:

  plot absolute values if \`TRUE\`

- title:

  title of plot

- ...:

  additional parameters

- x:

  object of class `module_kMEs`

- facetmodules:

  names of color modules to keep

- colormodules:

  names of color modules to keep

## Value

object of class \`module_kMEs\`

ggplot object

data frame
