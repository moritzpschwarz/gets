# Make Indicator Matrices (Impulses, Steps, Trends)

Auxiliary functions to make, respectively, matrices of impulse
indicators (`iim`), step indicators (`sim`) and trend indicators (`tim`)

## Usage

``` r
##make matrix of impulse indicators:
iim(x, which.ones = NULL)

##make matrix of step indicators:
sim(x, which.ones = NULL)

##make matrix of trend indicators:
tim(x, which.ones = NULL, log.trend = FALSE)
```

## Arguments

- x:

  either an integer (the length of the series in question) or a series
  (a vector or matrix) from which to use the time-series index to make
  indicators of

- which.ones:

  the locations of the impulses. If NULL (the default), then all
  impulses are returned

- log.trend:

  logical. If TRUE, then the natural log is applied on the trends

## Details

If `x` is a series or vector of observations, then the index of `x` will
be used for the labelling of the impulses, and in the returned
[`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) object.

Note: For `sim` and `tim` the first indicator is removed, since it is
exactly colinear with the others.

## Value

A [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) matrix containing the
impulses

## Author

Genaro Sucarrat, <http://www.sucarrat.net/>

## See also

[`isat`](http://moritzschwarz.org/gets/reference/isat.md),
[`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html)

## Examples

``` r
##generate series:
y <- rnorm(40)

##make matrix of impulse indicators:
mIIM <- iim(40)

##make matrix of step-indicators, but only every third:
mSIM <- sim(y, which.ones=seq(1,40,3))

##give quarterly time-series attributes to y-series:
y <- zooreg(y, frequency=4, end=c(2015,4))

##make matrix of trend-indicators with quarterly labels:
mTIM <- tim(y)
```
