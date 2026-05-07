# HARMOODS

**Harmonised Depression Score Converter** — an R Shiny application that places item-level responses from the HDRS, BDI, and MADRS onto a common latent severity metric using item response theory (IRT) graded response models.

[![Live demo](https://img.shields.io/badge/live%20demo-shinyapps.io-blue)](https://emmacorley.shinyapps.io/irt_app/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![R](https://img.shields.io/badge/R-4.3%2B-276DC3)](https://www.r-project.org/)

> **Live app:** [https://emmacorley.shinyapps.io/irt_app/](https://emmacorley.shinyapps.io/irt_app/)

## Overview

HARMOODS takes a CSV or Excel file of item-level responses from any combination of the **Hamilton Depression Rating Scale (HDRS)**, **Beck Depression Inventory (BDI)**, and **Montgomery–Åsberg Depression Rating Scale (MADRS)** and returns:

- An **IRT severity score (θ)** with standard error
- **Crosswalked totals** for each scale (the score a participant would have obtained had they been administered HDRS, BDI, or MADRS)
- **Raw observed sums** for completeness
- **QC, reliability, and correlation diagnostics** for inspection

Scores are produced for five symptom domains plus an **Overall Depression Severity** (general-factor) score:

| Domain | Description |
| --- | --- |
| Somatic | Sleep, appetite, fatigue, somatic anxiety |
| Anxiety | Worry, fear, hyperarousal |
| Cognitive Affective | Negative thoughts, low self-worth, emotional distress |
| Mood / Motivation | Mood fluctuations, anhedonia, energy |
| Overall Depression Severity | General depression factor |

## Why use HARMOODS

Multisite mood-disorder research often pools data from cohorts that used different depression rating scales. Sum-score conversions discard the differing item discrimination and threshold properties of each instrument. HARMOODS uses calibrated IRT graded response models so that a θ estimated from MADRS items is on the same metric as a θ estimated from BDI or HDRS items, making symptom severity directly comparable across studies.

The calibration models were fit in a multisite ENIGMA dataset of 11,171 individuals (6,417 healthy controls, 2,907 bipolar disorder, 1,847 major depressive disorder) across 47 international sites. Full details are reported in the accompanying manuscript.

## Run locally

```r
# 1. Install dependencies
install.packages(c(
  "shiny", "bslib", "readr", "readxl", "writexl",
  "dplyr", "tidyr", "tibble", "purrr", "stringr", "ggplot2"
))

# 2. Clone and run
# git clone https://github.com/emmajanecorley/harmoods.git
# cd harmoods
shiny::runApp(".")
```

The app opens in your browser. Upload a CSV/Excel with column names matching the expected items (e.g., `HDRS1`, `HDRS2`, …, `BDI1`, …, `MADRS1`, …) — column matching is fuzzy so `hdrs_1`, `hdrs.1`, or `HDRS-1` all resolve correctly.

## Input format

A wide-format file with one row per participant. Required columns are any subset of:

```
HDRS1 … HDRS17, HDRS_insomnia
BDI1  … BDI21
MADRS1 … MADRS10
```

Optional `SubjID` column for participant identifiers. An example file is provided in [`inst/example_data/`](inst/example_data/).

## Citation

If you use HARMOODS in published work, please cite:

> Corley E, et al. *Harmonizing depression severity scores: an item response theory investigation of brain structure from the ENIGMA Bipolar and Major Depressive Disorder Consortia.* (Manuscript in preparation, 2026)

A BibTeX entry is provided in [`CITATION.cff`](CITATION.cff).

## Disclaimer

HARMOODS is a research tool intended for psychometric harmonisation in research contexts. It does not provide clinical diagnoses, treatment recommendations, or individual-level clinical decision support. All outputs should be interpreted by qualified researchers within appropriate scientific and clinical context.

## Contributing

Issues and pull requests welcome. For substantive scientific questions or collaboration enquiries, please contact the corresponding author.

## Contact

**Emma Corley, PhD** — Clinical Neuroimaging Laboratory, University of Galway  
[emma.corley@universityofgalway.ie](mailto:emma.corley@universityofgalway.ie)

## License

MIT — see [LICENSE](LICENSE).
