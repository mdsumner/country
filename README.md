
<!-- README.md is generated from README.Rmd. Please edit that file -->
``` r
f <- "http://www.naturalearthdata.com/http//www.naturalearthdata.com/download/10m/cultural/ne_10m_admin_0_countries.zip"
download.file(f, basename(f), mode = "wb")
unzip(basename(f))
```

``` r
library(rgdal)
#> Loading required package: sp
#> rgdal: version: 1.1-10, (SVN revision 622)
#>  Geospatial Data Abstraction Library extensions to R successfully loaded
#>  Loaded GDAL runtime: GDAL 2.1.1, released 2016/07/07
#>  Path to GDAL shared files: /usr/share/gdal/2.1
#>  Loaded PROJ.4 runtime: Rel. 4.9.2, 08 September 2015, [PJ_VERSION: 492]
#>  Path to PROJ.4 shared files: (autodetected)
#>  Linking to sp version: 1.2-3
library(raster)
ctry <- readOGR(".", "ne_10m_admin_0_countries")
#> OGR data source with driver: ESRI Shapefile 
#> Source: ".", layer: "ne_10m_admin_0_countries"
#> with 255 features
#> It has 65 fields

fx <- function(x) (xmin(x) + xmax(x))/2
fy <- function(x) (ymin(x) + ymax(x))/2
projlocal <- function(x) {
  ## just the "middle" in longlat for now
  sprintf("+proj=laea +ellps=WGS84 +lon_0=%s +lat_0=f", fx(x), fy(x) )
}
```

``` r
op <- par(mar = rep(0, 4), xpd = NA)
for (irow in seq(nrow(ctry))[1:10]) {
  ## project to local based on first piece encountered
  x <- spTransform(ctry[irow, ], projlocal(disaggregate(ctry[irow, ])[1L, ]))
}

plot(ctry[irow, ]); llgridlines(ctry[irow, ])
```

![](README-unnamed-chunk-4-1.png)

``` r
plot(x); llgridlines(x)
```

![](README-unnamed-chunk-4-2.png)
