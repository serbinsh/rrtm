
<!-- README.md is generated from README.Rmd. Please edit that file -->

# rrtm

<!-- badges: start -->

<!-- badges: end -->

The goal of `rrtm` is to provide efficient R implementations of
radiative transfer models useful for vegetation remote sensing.

## Installation

`rrtm` is not currently on CRAN, but you can install the development
version of `rrtm` from [GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("ashiklom/rrtm")
```

## Basic usage

This is a basic example of running the PROSPECT 5 leaf radiative
transfer model.

``` r
library(rrtm)
out <- prospect5(1.4, 40, 10, 0.01, 0.01)
dim(out)
#> [1] 2101    1    2
plot(c(400, 2500), c(0, 1), type = "n",
     xlab = "Wavelength (nm)",
     ylab = "Spectra")
lines(400:2500, out[,,1], col = "red")
lines(400:2500, 1 - out[,,2], col = "blue")
legend("top", legend = c("reflectance", "1 - transmittance"),
       lty = 1, col = c("red", "blue"))
```

<img src="man/figures/README-basic-1.png" width="100%" />

Note that the returned object has 3 dimensions, not 2. This reflects a
unique feature of this package: Support for multi-dimensional radiative
transfer calculations. All of the `prospectX` functions can take vectors
as inputs and will return multi-dimensional arrays as outputs.

``` r
out2 <- prospect4(1.4, c(30, 40, 50), c(0.01, 0.005, 0.002), 0.01)
plot(c(400, 2500), c(0, 1), type = 'n',
     xlab = "Wavelength (nm)",
     ylab = "Spectra")
matplot(400:2500, f[,,1], type = "l", add = TRUE)
matplot(400:2500, 1 - f[,,2], type = "l", add = TRUE)
```

<img src="man/figures/README-multi-1.png" width="100%" />
