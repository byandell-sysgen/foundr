# Title

Trait names are distinct within a dataset, but may be duplicated in
different datasets (for instance same type of trait in two tissues). The
\`object\` will have a column \`dataset\` if it comprises multiple
datasets, but it is also possible that the \`dataset\` column is absent
(in case there is only one dataset).

## Usage

``` r
trait_names(object, traitnames = NULL, sep = ": ")
```

## Arguments

- object:

  data frame or object containing dataset and trait columns

- traitnames:

  names of traits, possibly including dataset name with separator

- sep:

  separator character(s) between dataset and trait name

## Value

vector of trait names prepended by dataset if appropriate

## Details

The argument \`traitnames\` can be one of the following: 1. names found
in \`trait\` column that are distinct across any possible datasets. 2.
name of the form \`dataset: trait\`, that is, separated by the \`sep\`
string. 3. data frame with columns for \`dataset\` and \`trait\`, with
one row entry per traitname. 4. NULL, in which case all \`datatraits\`
in \`object\` are returned

## Examples

``` r
trait_names(sampleData, c("A","C"))
#> [1] "sample: C" "sample: A"
```
