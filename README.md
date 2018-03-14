
<!-- README.md is generated from README.Rmd. Please edit that file -->
[![Build Status](https://travis-ci.org/marcosci/nlmr.svg?branch=develop)](https://travis-ci.org/marcosci/nlmr) [![Build status](https://ci.appveyor.com/api/projects/status/ns75pdrbaykxc865?svg=true)](https://ci.appveyor.com/project/marcosci/nlmr) [![codecov](https://codecov.io/gh/marcosci/nlmr/branch/develop/graph/badge.svg?token=MKCm2fVrDa)](https://codecov.io/gh/marcosci/nlmr) [![CRAN\_Status\_Badge](http://www.r-pkg.org/badges/version/nlmr)](https://cran.r-project.org/package=nlmr) [![Join the chat at https://gitter.im/nlmr\_landscapegenerator](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/nlmr_landscapegenerator) [![](http://cranlogs.r-pkg.org/badges/grand-total/nlmr)](http://cran.rstudio.com/web/packages/nlmr/index.html) [![](https://badges.ropensci.org/188_status.svg)](https://github.com/ropensci/onboarding/issues/188)

nlmr <img src="vignettes/logo.png" align="right"  height="175" />
=================================================================

`nlmr` is an `R` package for simulating **n**eutral **l**andscape **m**odels (NLM). Designed to be a generic framework like [NLMpy](https://pypi.python.org/pypi/nlmpy), it leverages the ability to simulate the most common NLM that are described in the ecological literature. `nlmr` builds on the advantages of the `raster`-package and returns all simulation as `RasterLayer`-objects, thus ensuring a direct compability to common GIS tasks and a pretty flexible and simple usage. Furthermore, it simulates NLMs within a self-contained, reproducible framework.

<img src="vignettes/nlmr_grid.png"  width="100%" />

<br>

Installation
------------

Install the release version from CRAN:

``` r
install.packages("nlmr")
```

To install the developmental version of `nlmr`, use the following R code:

``` r
# install.packages("devtools")
devtools::install_github("marcosci/nlmr", ref = "develop")
```

Example
-------

Here we will provide a simple example on using `nlmr`:

``` r
library(nlmr)
library(magrittr)
library(ggplot2)  # to extend the plot functionality of nlmr 
library(SDMTools) # to calculate basic landscape metrics

# Simulate 50x50 rectangular cluster raster
nlm_raster <- nlm_randomrectangularcluster(50,50, resolution = 1, minl = 3, maxl = 7)

# Plot the NLM
util_plot(nlm_raster) +
  labs(title="Random rectangular cluster NLM \n (50x50 cells)")
#> Warning in seq.default(.limits[1], .limits[2], length = guide$nbin):
#> partial argument match of 'length' to 'length.out'
```

<img src="vignettes/README-unnamed-chunk-4-1.png" style="display: block; margin: auto;" />

``` r

# Classify into 3 categories
nlm_raster <- nlm_raster %>%
                 util_classify(., c(0.5, 0.25, 0.25))

# Plot the classified NLM
util_plot(nlm_raster, discrete = TRUE) +
  labs(title="Random rectangular cluster NLM \n (50x50 cells)")
```

<img src="vignettes/README-unnamed-chunk-4-2.png" style="display: block; margin: auto;" />

``` r

# Calculate basic landscape metrics
raster::as.matrix(nlm_raster) %>% 
  PatchStat() %>% 
  knitr::kable()
```

|  patchID|  n.cell|  n.core.cell|  n.edges.perimeter|  n.edges.internal|  area|  core.area|  perimeter|  perim.area.ratio|  shape.index|  frac.dim.index|  core.area.index|
|--------:|-------:|------------:|------------------:|-----------------:|-----:|----------:|----------:|-----------------:|------------:|---------------:|----------------:|
|        0|    1239|          526|                836|              4120|  1239|        526|        836|         0.6747377|     5.887324|        1.500222|        0.4245359|
|        1|     632|          182|                598|              1930|   632|        182|        598|         0.9462025|     5.862745|        1.552917|        0.2879747|
|        2|     629|          202|                566|              1950|   629|        202|        566|         0.8998410|     5.549020|        1.536995|        0.3211447|

Meta
----

-   Please [report any issues or bugs](https://github.com/marcosci/nlmr/issues/new/).
-   License: GPL3
-   Get citation information for `nlmr` in R doing `citation(package = 'nlmr')`
    -   Additionally, we keep a [record of publications](https://marcosci.github.io/nlmr/articles/publication_record.html/) that use`nlmr`. Hence, if you used `nlmr` please [file an issue on GitHub](https://github.com/marcosci/nlmr/issues/new/) so we can add it to the list.
-   We are very open to contributions - if you are interested check [Contributor Code of Conduct](CONTRIBUTING.md).
    -   Please note that this project is released with a [Contributor Code of Conduct](CONDUCT.md). By participating in this project you agree to abide by its terms.

Dependencies
------------

`nlmr` imports many great packages that it depends on. Many thanks to the developers of these tools:

     [1] "R (>= 3.1.0)"  " checkmate"    " dismo"        " dplyr"       
     [5] " ggplot2"      " igraph"       " magrittr"     " purrr"       
     [9] " RandomFields" " raster"       " rasterVis"    " sp"          
    [13] " spatstat"     " stats"        " tibble"       " tidyr"       
    [17] " viridis"      " extrafont"
