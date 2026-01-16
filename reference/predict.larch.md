# Variance forecasting with 'larch' models

Generate out-of-sample variance forecasts up to `n.ahead` steps ahead.
Optionally, quantiles of the forecasts are also returned if the argument
`probs` is specified. The forecasts, confidence intervals and quantiles
are obtained via simulation. By default, 5000 simulations is used, but
this can be changed via the `n.sim` argument. Also by default, the
simulations uses a classical bootstrap to sample from the standardised
residuals. To use an alternative set of standardised innovations, for
example the standard normal, use the `innov` argument

## Usage

``` r
# S3 method for class 'larch'
predict(object, n.ahead=12, newvxreg=NULL, newindex=NULL, 
    n.sim=NULL, innov=NULL, probs=NULL, quantile.type=7, verbose = FALSE, ...)
```

## Arguments

- object:

  an object of class 'larch'

- n.ahead:

  `integer` that determines how many steps ahead predictions should be
  generated (the default is 12)

- newvxreg:

  a `matrix` of `n.ahead` rows and `NCOL(vxreg)` columns with the
  out-of-sample values of the `vxreg` regressors

- newindex:

  `NULL` (default) or the date-index for the
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) object returned by
  `predict.larch`. If `NULL`, then the function uses the in-sample
  `index` to generate the out-of-sample index

- n.sim:

  `NULL` (default) or an `integer`, the number of replications used for
  the generation of the forecasts. If `NULL`, the number of simulations
  is determined internally (usually 5000)

- innov:

  `NULL` (default) or a vector of length `n.ahead * n.sim` containing
  the standardised errors (i.e. mean zero and unit variance) used for
  the forecast simulations. If `NULL`, then a classic bootstrap
  procedure is used to draw from the standardised in-sample residuals

- probs:

  `NULL` (default) or a `vector` with the quantile-levels (values
  strictly between 0 and 1) of the forecast distribution. If `NULL`,
  then no quantiles are returned

- quantile.type:

  an integer between 1 and 9 that selects which algorithm to be used in
  computing the quantiles, see the argument `type` in
  [`quantile`](https://rdrr.io/r/stats/quantile.html)

- verbose:

  logical with default `FALSE`. If `TRUE`, then additional information
  (typically the quantiles and/or the simulated series) used in the
  generation of forecasts is returned. If `FALSE`, then only the
  forecasts are returned

- ...:

  additional arguments

## Value

a `vector` of class [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html)
containing the out-of-sample forecasts, or a `matrix` of class
[`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) containing the
out-of-sample forecasts together with additional information (e.g. the
prediction-quantiles)

## Details

No details for the moment.

## Author

Genaro Sucarrat, <https://www.sucarrat.net/>

## See also

[`larch`](http://moritzschwarz.org/gets/reference/larch.md)

## Examples

``` r
##Simulate some data:
set.seed(123)
e <- rnorm(40)

##estimate log-ARCH(1) model:
mymod <- larch(e, arch=1)

##generate out-of-sample forecasts:
predict(mymod)
#>        41        42        43        44        45        46        47        48 
#> 0.8170129 0.7904251 0.7891456 0.7900300 0.7893880 0.7912624 0.7874184 0.7931848 
#>        49        50        51        52 
#> 0.7909795 0.7920767 0.7898949 0.7908645 

##same, but return also selected quantiles:
predict(mymod, probs=c(0.10,0.90))
#>          sd2      q0.1      q0.9
#> 41 0.8170129 0.8170129 0.8170129
#> 42 0.7889723 0.7047023 0.8926209
#> 43 0.7914196 0.7082388 0.9141842
#> 44 0.7918035 0.7081293 0.9142889
#> 45 0.7918120 0.7100031 0.9176080
#> 46 0.7898864 0.7082053 0.9176523
#> 47 0.7914346 0.7092270 0.9121551
#> 48 0.7908053 0.7075605 0.9120371
#> 49 0.7906303 0.7056429 0.9140266
#> 50 0.7900909 0.7073553 0.9176142
#> 51 0.7894340 0.7066438 0.8989683
#> 52 0.7908136 0.7075815 0.9176056

##same, but using standard normals (instead of bootstrap) in the simulations:
n.sim <- 2000
n.ahead <- 12 #the default on n.ahead
predict(mymod, probs=c(0.10,0.90), n.sim=n.sim, innov=rnorm(n.ahead*n.sim))
#>          sd2      q0.1      q0.9
#> 41 0.8170129 0.8170129 0.8170129
#> 42 0.8042051 0.7110091 0.9296428
#> 43 0.8043217 0.7116390 0.9266204
#> 44 0.8035386 0.7129277 0.9195822
#> 45 0.8029674 0.7115389 0.9169221
#> 46 0.8027409 0.7117134 0.9186196
#> 47 0.8018033 0.7109971 0.9221035
#> 48 0.8058531 0.7123469 0.9229128
#> 49 0.8056665 0.7118974 0.9271428
#> 50 0.8044520 0.7134699 0.9295316
#> 51 0.8068406 0.7127420 0.9309104
#> 52 0.8057668 0.7117767 0.9252066

##make x-regressors:
x <- matrix(rnorm(40*2), 40, 2)

##estimate log-ARCH(1) model w/covariates:
mymod <- larch(e, arch=1, vxreg=x)

##predict up to 5 steps ahead, setting x's to 0 out-of-sample:
predict(mymod, n.ahead=5, newvxreg=matrix(0,5,NCOL(x)))
#>        41        42        43        44        45 
#> 0.8036733 0.7764522 0.7796526 0.7778416 0.7774535 
```
