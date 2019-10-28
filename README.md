
<!-- README.md is generated from README.Rmd. Please edit that file -->

# codex

<!-- badges: start -->

[![Appveyor build
status](https://ci.appveyor.com/api/projects/status/xxx/branch/master?svg=true)](https://ci.appveyor.com/project/nfrerebeau/codex/branch/master)
[![Travis build
Status](https://travis-ci.org/nfrerebeau/codex.svg?branch=master)](https://travis-ci.org/nfrerebeau/codex)
[![codecov](https://codecov.io/gh/nfrerebeau/codex/branch/master/graph/badge.svg)](https://codecov.io/gh/nfrerebeau/codex)

[![CRAN
Version](http://www.r-pkg.org/badges/version/codex)](https://cran.r-project.org/package=codex)
[![CRAN
checks](https://cranchecks.info/badges/worst/codex)](https://cran.r-project.org/web/checks/check_results_codex.html)
[![CRAN
Downloads](http://cranlogs.r-pkg.org/badges/codex)](https://cran.r-project.org/package=codex)

[![Project Status: Active – The project has reached a stable, usable
state and is being actively
developed.](https://www.repostatus.org/badges/latest/wip.svg)](https://www.repostatus.org/#wip)
[![Lifecycle:
experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://www.tidyverse.org/lifecycle/#experimental)

[![DOI](https://zenodo.org/badge/DOI/xxx.svg)](https://doi.org/xxx)
<!-- badges: end -->

## Overview

A collection of classes that represent archaeological data. This package
provides a set of S4 classes that extend the basic matrix data type and
a set of generic methods and functions. In addition, a few classes of
general interest (e.g. that represent time and space information) are
implemented.

## Installation

<!--You can install the released version of **codex** from [CRAN](https://CRAN.R-project.org) with:


```r
install.packages("codex")
```

Or-->

You can install the development version from GitHub with:

``` r
# install.packages("devtools")
remotes::install_github("nfrerebeau/codex")
```

## Usage

``` r
# Load package
library(codex)
```

### Matrix

**codex** provides a set of S4 classes that extend the basic `matrix`
data type. These new classes represent different special types of
matrix.

  - Abundance matrix:
      - `CountMatrix` represents count data,
      - `FrequencyMatrix` represents relative frequency data.
  - Logical matrix:
      - `IncidenceMatrix` represents presence/absence data.
  - Other numeric matrix:
      - `OccurrenceMatrix` represents a co-occurrence matrix.
      - `SimilarityMatrix` represents a (dis)similarity matrix.

*It assumes that you keep your data tidy*: each variable (type/taxa)
must be saved in its own column and each observation (sample/case) must
be saved in its own row.

These new classes are of simple use, on the same way as the base
`matrix`:

``` r
# Define a count data matrix
quanti <- CountMatrix(data = sample(0:10, 100, TRUE),
                      nrow = 10, ncol = 10)

# Define a logical matrix
# Data will be coerced with as.logical()
quali <- IncidenceMatrix(data = sample(0:1, 100, TRUE),
                         nrow = 10, ncol = 10)
```

**codex** uses coercing mechanisms (with validation methods) for data
type conversions:

``` r
## Create a count matrix
A1 <- CountMatrix(data = sample(0:10, 100, TRUE),
                  nrow = 10, ncol = 10)

## Coerce counts to frequencies
B <- as_frequency(A1)

## Row sums are internally stored before coercing to a frequency matrix
## (use totals() to get these values)
## This allows to restore the source data
A2 <- as_count(B)
all(A1 == A2)
#> [1] TRUE

## Coerce to presence/absence
C <- as_incidence(A1)

## Coerce to a co-occurrence matrix
D <- as_occurrence(A1)
```

## Contributing

Please note that the **codex** project is released with a [Contributor
Code of
Conduct](https://github.com/nfrerebeau/codex/blob/master/.github/CODE_OF_CONDUCT.md).
By contributing to this project, you agree to abide by its terms.
