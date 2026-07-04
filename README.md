# Longitudinal Modelling of the ARMD Clinical Trial

Linear mixed-effects analysis of visual-acuity decline in the Age-Related Macular
Degeneration (ARMD) trial, comparing an active treatment (interferon alfa-2a) against
placebo over one year.

## Overview

In the ARMD trial, visual acuity (number of letters read correctly) was measured at
baseline and at 4, 12, 24, and 52 weeks. This analysis works with a random 150-patient
subsample and asks whether the active treatment slows the loss of vision. It builds up
from marginal (GLS) models of the mean and covariance structure to linear mixed-effects
models with subject-level random effects.

## Data

`armd` / `armd.wide` from the **nlmeU** R package (Gałecki & Burzykowski, 2013). No
external data file is required — the dataset ships with the package. A fixed random seed
selects the working subsample (148 subjects and 553 observations after excluding subjects
with no post-baseline measurements). Missingness is monotone for most patients and is
treated as MAR, with models fitted by maximum likelihood.

## Methods

- Exploratory analysis of mean profiles and missing-data patterns.
- Marginal models via generalised least squares (`gls`): a power-of-time variance
  function and successively richer within-subject correlation structures (compound
  symmetry, then unstructured), compared by likelihood-ratio tests.
- Linear mixed-effects models (`lme`): random intercept, then random intercept + slope,
  with a power variance function on the residuals.
- Model selection by AIC/BIC; the treatment effect tested with a likelihood-ratio test
  against a reduced model; residual and Q–Q diagnostics.

## Key results

The final model (random intercept and slope, time-dependent residual variance) placed
roughly half the total variation between patients (ICC ≈ 0.50). The treatment effect was
**not significant** (likelihood-ratio test, p = 0.36): interferon alfa-2a did not slow
visual-acuity decline in this subsample, consistent with the published trial and the
textbook case study.

## Repository contents

- `analysis.Rmd` — full analysis source (R code and commentary)
- `report.pdf` — rendered report
- `README.md`

## Running the analysis

Requires R with `nlme`, `nlmeU`, and `lattice`. Knit `analysis.Rmd` in RStudio, or run the
extracted R code. No external data is needed.

## Notes

Developed during my MSc in Bioinformatics and Biostatistics. Report and code comments are
in Spanish; this README summarises the work in English.
