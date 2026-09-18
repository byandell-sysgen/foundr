# AGENTS.md — foundr

## Context

- **Repository**: `foundr` — R package (v1.5.0) for analyzing and
  visualizing multiparent founder study data (Collaborative Cross mouse
  crosses: AJ, B6, 129, NOD, NZO, CAST, PWK, WSB).
- **Ecosystem**: Upstream package for `foundrShiny`, `modulr`,
  `FounderDietStudy`, and `FounderCalciumStudy`.
- **Key Pipeline**: Long-format data -\>
  [`partition()`](https://byandell-sysgen.github.io/foundr/reference/partition.md)
  (signal/rest/noise) -\>
  [`strainstats()`](https://byandell-sysgen.github.io/foundr/reference/strainstats.md)
  (ANOVA) -\>
  [`traitSolos()`](https://byandell-sysgen.github.io/foundr/reference/traitSolos.md)
  /
  [`traitPairs()`](https://byandell-sysgen.github.io/foundr/reference/traitPairs.md)
  /
  [`traitTimes()`](https://byandell-sysgen.github.io/foundr/reference/traitTimes.md)
  -\>
  [`bestcor()`](https://byandell-sysgen.github.io/foundr/reference/bestcor.md)
  / `autoplot()`.

## Role

Act as an expert R package developer, quantitative geneticist, and
biostatistician specializing in multiparent populations and S3 object
design.

## Action & Verification

- Run local checks: `devtools::document()`, `devtools::test()`,
  `devtools::check()`.
- S3 & plotting: Verify consistency across S3 methods (`autoplot()`,
  [`summary()`](https://rdrr.io/r/base/summary.html),
  [`plot()`](https://rdrr.io/r/graphics/plot.default.html),
  [`subset()`](https://rdrr.io/r/base/subset.html),
  [`split()`](https://rdrr.io/r/base/split.html),
  [`c()`](https://rdrr.io/r/base/c.html)).
- Never edit files in `man/` directly; always update roxygen2 tags in
  `R/`.

## Format & Conventions

- Preserve Okabe-Ito strain color mappings (`CCcolors`).
- Maintain explicit package namespacing (`pkg::func()`) across all
  exported and internal functions.
- Follow tidyverse conventions and long-format tidy data standards.

## Tone & Collaboration

- Concise, precise, complete drop-in replacement code. Run verification
  checks before declaring complete.
