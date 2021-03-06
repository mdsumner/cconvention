
[![Travis-CI Build Status](https://travis-ci.org/mdsumner/cconvention.svg?branch=master)](https://travis-ci.org/mdsumner/cconvention) [![AppVeyor Build Status](https://ci.appveyor.com/api/projects/status/github/mdsumner/cconvention?branch=master&svg=true)](https://ci.appveyor.com/project/mdsumner/cconvention) [![Coverage Status](https://img.shields.io/codecov/c/github/mdsumner/cconvention/master.svg)](https://codecov.io/github/mdsumner/cconvention?branch=master)

<!-- README.md is generated from README.Rmd. Please edit that file -->
cconvention
===========

The goal of cconvention is to provide access to the CCAMLR convention in spatial form, from scratch.

Installation
------------

You can install cconvention from github with:

``` r
# install.packages("devtools")
devtools::install_github("mdsumner/cconvention")
```

Work in progress
----------------

This project aims to collate the agreed boundaries define by CCAMLR.

-   The `division` functions shows a manual way of doing this, encoding the path steps taken to define boundary lines
-   the `parse-text` vignette uses `Combin8R` to begin building an automated tool for extracting the information from the text

Either method results in a 1D topology, the connected boundaries in raw geographic space that need to be "baked-in", both by introducing intermediate vertices to carry curvature and to integrate implicit physical boundaries specied in the text, such as "coastline" or "ice shelf".

After baking, we can provide easy to use map structures for analytical work. The main advantage to using this process is to avoid artefacts introduced by inexact geo-spatial operations.

Example
-------

This is a basic example which loads an in-built data set.

``` r
library(cconvention)
subarea <- division()

library(sp)
library(rgdal)
#> rgdal: version: 1.2-4, (SVN revision 643)
#>  Geospatial Data Abstraction Library extensions to R successfully loaded
#>  Loaded GDAL runtime: GDAL 2.0.1, released 2015/09/15
#>  Path to GDAL shared files: C:/Users/mdsumner/Documents/R/win-library/3.3/rgdal/gdal
#>  Loaded PROJ.4 runtime: Rel. 4.9.2, 08 September 2015, [PJ_VERSION: 492]
#>  Path to PROJ.4 shared files: C:/Users/mdsumner/Documents/R/win-library/3.3/rgdal/proj
#>  Linking to sp version: 1.2-3
p <- spTransform(subarea, "+proj=laea +lon_0=147 +lat_0=-90 +ellps=WGS84 +no_defs")
plot(p, col = "darkgrey")
```

![](README-example-1.png)
