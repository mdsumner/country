---
output: rmarkdown::html_vignette
---

<!-- README.md is generated from README.Rmd. Please edit that file -->




```r
f <- "http://www.naturalearthdata.com/http//www.naturalearthdata.com/download/10m/cultural/ne_10m_admin_0_countries.zip"
download.file(f, basename(f), mode = "wb")
unzip(basename(f))
```


```r
library(rgdal)
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


```r
ef <- 1.4
op <- par(mar = rep(0, 4), xpd = NA, cex = 0.8)
for (irow in seq(nrow(ctry))) {
  ## project to local based on first piece encountered
  x <- try(spTransform(ctry[irow, ], projlocal(disaggregate(ctry[irow, ])[1L, ])))
  if (inherits(x, "try-error")) {
    print(sprintf("ba bom %s", ctry$SOVEREIGNT[irow]))
    } else {
  plot(extent(ctry[irow, ]) * ef, type = "n", axes = FALSE, xlab = "", ylab = "", main = x$SOVEREIGNT[irow])
  plot(ctry[irow, ], add = TRUE); llgridlines(ctry[irow, ], col = "lightgrey", lty = 2)
  plot(extent(x) * ef, type = "n", axes = FALSE, xlab = "", ylab = "")
plot(x, add = TRUE); try(llgridlines(x, col = "lightgrey", lty = 2))
}}
```

![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-1.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-2.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-3.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-4.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-5.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-6.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-7.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-8.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-9.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-10.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-11.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-12.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-13.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-14.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-15.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-16.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-17.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-18.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-19.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-20.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-21.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-22.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-23.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-24.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-25.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-26.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-27.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-28.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-29.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-30.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-31.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-32.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-33.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-34.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-35.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-36.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-37.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-38.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-39.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-40.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-41.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-42.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-43.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-44.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-45.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-46.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-47.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-48.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-49.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-50.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-51.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-52.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-53.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-54.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-55.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-56.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-57.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-58.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-59.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-60.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-61.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-62.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-63.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-64.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-65.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-66.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-67.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-68.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-69.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-70.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-71.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-72.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-73.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-74.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-75.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-76.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-77.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-78.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-79.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-80.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-81.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-82.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-83.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-84.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-85.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-86.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-87.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-88.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-89.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-90.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-91.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-92.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-93.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-94.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-95.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-96.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-97.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-98.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-99.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-100.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-101.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-102.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-103.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-104.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-105.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-106.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-107.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-108.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-109.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-110.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-111.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-112.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-113.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-114.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-115.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-116.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-117.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-118.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-119.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-120.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-121.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-122.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-123.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-124.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-125.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-126.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-127.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-128.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-129.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-130.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-131.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-132.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-133.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-134.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-135.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-136.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-137.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-138.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-139.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-140.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-141.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-142.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-143.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-144.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-145.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-146.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-147.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-148.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-149.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-150.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-151.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-152.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-153.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-154.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-155.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-156.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-157.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-158.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-159.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-160.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-161.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-162.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-163.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-164.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-165.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-166.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-167.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-168.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-169.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-170.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-171.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-172.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-173.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-174.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-175.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-176.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-177.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-178.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-179.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-180.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-181.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-182.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-183.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-184.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-185.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-186.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-187.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-188.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-189.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-190.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-191.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-192.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-193.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-194.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-195.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-196.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-197.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-198.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-199.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-200.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-201.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-202.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-203.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-204.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-205.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-206.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-207.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-208.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-209.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-210.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-211.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-212.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-213.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-214.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-215.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-216.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-217.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-218.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-219.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-220.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-221.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-222.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-223.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-224.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-225.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-226.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-227.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-228.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-229.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-230.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-231.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-232.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-233.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-234.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-235.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-236.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-237.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-238.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-239.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-240.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-241.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-242.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-243.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-244.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-245.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-246.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-247.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-248.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-249.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-250.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-251.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-252.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-253.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-254.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-255.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-256.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-257.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-258.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-259.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-260.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-261.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-262.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-263.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-264.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-265.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-266.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-267.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-268.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-269.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-270.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-271.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-272.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-273.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-274.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-275.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-276.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-277.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-278.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-279.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-280.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-281.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-282.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-283.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-284.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-285.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-286.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-287.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-288.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-289.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-290.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-291.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-292.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-293.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-294.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-295.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-296.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-297.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-298.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-299.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-300.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-301.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-302.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-303.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-304.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-305.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-306.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-307.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-308.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-309.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-310.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-311.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-312.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-313.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-314.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-315.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-316.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-317.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-318.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-319.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-320.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-321.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-322.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-323.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-324.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-325.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-326.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-327.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-328.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-329.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-330.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-331.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-332.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-333.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-334.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-335.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-336.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-337.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-338.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-339.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-340.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-341.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-342.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-343.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-344.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-345.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-346.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-347.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-348.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-349.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-350.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-351.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-352.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-353.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-354.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-355.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-356.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-357.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-358.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-359.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-360.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-361.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-362.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-363.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-364.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-365.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-366.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-367.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-368.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-369.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-370.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-371.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-372.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-373.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-374.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-375.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-376.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-377.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-378.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-379.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-380.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-381.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-382.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-383.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-384.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-385.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-386.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-387.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-388.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-389.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-390.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-391.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-392.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-393.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-394.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-395.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-396.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-397.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-398.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-399.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-400.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-401.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-402.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-403.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-404.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-405.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-406.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-407.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-408.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-409.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-410.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-411.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-412.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-413.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-414.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-415.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-416.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-417.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-418.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-419.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-420.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-421.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-422.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-423.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-424.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-425.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-426.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-427.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-428.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-429.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-430.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-431.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-432.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-433.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-434.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-435.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-436.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-437.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-438.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-439.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-440.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-441.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-442.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-443.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-444.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-445.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-446.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-447.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-448.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-449.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-450.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-451.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-452.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-453.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-454.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-455.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-456.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-457.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-458.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-459.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-460.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-461.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-462.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-463.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-464.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-465.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-466.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-467.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-468.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-469.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-470.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-471.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-472.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-473.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-474.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-475.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-476.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-477.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-478.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-479.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-480.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-481.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-482.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-483.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-484.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-485.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-486.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-487.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-488.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-489.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-490.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-491.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-492.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-493.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-494.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-495.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-496.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-497.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-498.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-499.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-500.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-501.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-502.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-503.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-504.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-505.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-506.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-507.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-508.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-509.png)![plot of chunk unnamed-chunk-4](figure/README-unnamed-chunk-4-510.png)
