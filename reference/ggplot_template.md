# GGplot template for other routines

This routine is used by multiple others (\`traitSolos\`, \`traitPairs\`,
\`traitTimes\`), providing one place for specialized plotting code to
avoid duplication and improve visualization. However, it has some quirks
to meet all needs. See details.

## Usage

``` r
ggplot_template(object, ..., drop_xlab = FALSE, legend_position = "bottom")
```

## Arguments

- object:

  list of data frames to be plotted

- ...:

  additional parameters

- drop_xlab:

  drop \`xlab\` except last if \`TRUE\`

- legend_position:

  show legend if \`TRUE\`

- facet_strain:

  facet by strain if \`TRUE\`

- shape_sex:

  use different shape by sex if \`TRUE\`

- boxplot:

  overlay boxplot if \`TRUE\`

## Value

object of class ggplot

## Details

The template consists of a wrapper (\`ggplot_template\`) to make
multiple calls to create individual ggplot objects (\`ggplot_onerow\`).
The \`object\` is a list constructed by other routines
(\`ggpot_traitSolos\`, \`ggplot_traitPairs\`, \`ggplot_traitTimes\`) in
distinct ways. Signals are passed in subtle ways about how the routines
are adapted for distinct uses:

- shape_sexdifferent shapes by \`sex\` if \`TRUE\` (all)

- facet_strainfacet by \`strain\` if \`TRUE\` (Solos, Pairs); used in
  tricky ways for Times

- legend_position"none" (Solos, Pairs) or "bottom" (Times)

- drop_xlabdrop xlab from all but last ggplot object (Solos, Times)

- parallel_lines

Other peculiarities are more deeply embedded in attributes either to the
\`object\` or to the elements of the list in \`object.\`

- traitnamestrait names as \`dataset: trait\` (\`object\` for all)

- response"value","cellmean","signal" (Solos,Pairs)

- smooth_method"lm" (Solos,Pairs), "loess" (timetype == "strain";
  Times), "line" (timetype == "stats"; Times)

- pairpair of traits (Pairs), "time" and trait name (Times)

- sepseparator " ON " (Pairs)

- timetype"strain","stats" (Times)

- time"minute","week" (timetype == "strain") or
  "minute_summary","week_summary" (timetype == "stats") (Times)

In addition the presence or absence of a column for "condition" affects
whether faceting or coloring is based on "sex" or "sex_condition".
Typically, parameter \`facet_strain\` controls facet vs color: if
\`TRUE\`, facet by \`strain\` and color by \`sex\` and \`condition\`; if
\`FALSE\` facet by \`sex\` and \`condition\` and color by \`strain\`;
however, if a Times plot with \`response\` == "value", then color by
\`strain\`.
