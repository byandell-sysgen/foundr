# Unite Dataset and Trait

This operates in different ways based on \`undo\`. Need to use both
\`dataset\` and \`trait\` to identify data for a \`trait\`.

## Usage

``` r
unite_datatraits(
  object,
  traitnames,
  undo = FALSE,
  sep = ": ",
  filters = NULL,
  key = FALSE
)
```

## Arguments

- object:

  data frame

- traitnames:

  names as \`dataset: trait\` for subsetting (when \`undo\` = \`TRUE\`)

- undo:

  logical flag on function use

- sep:

  separator for \`dataset: trait\` (default ": ")

- filters:

  optional list of columns to filter on (when \`undo\` = \`FALSE\`)

- key:

  get key traits if \`TRUE\`

## Value

either a subset \`object\` based on \`traitnames\` = \`dataset: trait\`
(if \`undo\` = \`TRUE\`) or vector of \`dataset: trait\` names (if
\`undo\` = \`FALSE\`, default)
