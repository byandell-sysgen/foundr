# Use Broom to Find Stats for Model Summaries

Use Broom to Find Stats for Model Summaries

Summary of Strain Statistics

## Usage

``` r
strainstats(
  object,
  signal = ifelse(is_condition, paste("strain * sex *", condition_name), "strain * sex"),
  rest = ifelse(is_condition, paste("strain * sex + sex *", condition_name), "sex"),
  calc_sd = TRUE,
  condition_name = "condition",
  ...
)

summary_strainstats(
  object,
  terms = termsnow,
  stats = c("deviation", "log10.p"),
  model = c("parts", "terms"),
  threshold = c(SD = 1, p.value = 0.01),
  ...
)

# S3 method for class 'strainstats'
summary(object, ...)
```

## Arguments

- object:

  object of class \`strainstats\`

- signal:

  signal factor combination as string for \`formula\`

- rest:

  rest factor combination as string for \`formula\`

- calc_sd:

  calculate SDs by \`term\` if \`TRUE\` (default)

- condition_name:

  name of \`condition\` column if present.

- ...:

  not used

- terms:

  terms to include (overrides \`model\` and \`stats\`)

- stats:

  choice of \`deviation\` or \`log10.p\`

- model:

  choice of model \`parts\` or \`terms\`

- threshold:

  named vector for \`SD\` and \`p.value\`

## Value

data frame with summaries by trait

data frame

## Examples

``` r
out <- strainstats(sampleData)
summary(out, "deviation", "parts")
#> Error in summary_strainstats(object, ...): object 'out' not found
summary(out, "log10.p", "terms")
#> Error in summary_strainstats(object, ...): object 'out' not found
```
