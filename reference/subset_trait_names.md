# Subset Trait Data on Names

Trait names of form \`dataset: trait\` will be selected.

## Usage

``` r
subset_trait_names(
  object,
  traitnames = NULL,
  remove_columns = FALSE,
  drop_united = TRUE,
  sep = ": "
)
```

## Arguments

- object:

  data frame

- traitnames:

  character string

- remove_columns:

  remove columns \`dataset\` and \`trait\` if \`TRUE\`

- drop_united:

  drop \`datatraits\` if \`TRUE\`

- sep:

  separator string

## Value

data frame
