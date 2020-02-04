---
output: github_document
---

# Assignment tests

Use a bunch of assignment tests programs to perform efficient and optimal assignment test.

## 1. Install `radiator` using `devtools` package

```r
if (!require("devtools")) install.packages("devtools")
devtools::install_github("thierrygosselin/radiator")
library(radiator)
```

## 2. Install `assigner` package

```r
if (!require("devtools")) install.packages("devtools")
devtools::install_github("thierrygosselin/assigner")
library(assigner)
```

### Import vcf data using `radiator`

```r
tidy_sebastes <- tidy_genomic_data(data="24603snps_416ind_mentella.recode.vcf", strata = "population_map_groups_mentella.txt", filename = NULL)
```

### Perform assignment test with `radiator`

Use the following parameters:
- markers.sampling = "ranked" 
We want to detect the number of markers we need to accurately assign individuals then we need to raked the markers from the most to the less discriminant.

- assignment.analysis = gis_sim 
[Gis_sim](https://github.com/eriqande/gsi_sim) is a software designed specially to perform "Genetic Stock Identification" (GSI).

- thl = 0.5
This option is for markers.sampling = "ranked" only. Here 50 percent of the individuals, in each strata, are chosen randomly as holdout individuals in order to overestimate the sucess of the assignment.

In R you can run.
```r
test1 <- assigner::assignment_ngs(
  data = tidy_sebastes, 
  markers.sampling = "ranked",
  assignment.analysis = "gsi_sim",
  sampling.method = "ranked", 
  thl = 0.5)
```