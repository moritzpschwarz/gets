# Consistency and Efficiency Correction for Impulse Indicator Saturation

Takes an [`isat`](http://moritzschwarz.org/gets/reference/isat.md)
object and corrects the estimates of the error variance and the
estimated standard errors of 'forced' regressors.

## Usage

``` r
isatvarcorrect(x, mcor=1)
```

## Arguments

- x:

  an [`isat`](http://moritzschwarz.org/gets/reference/isat.md) object

- mcor:

  integer, number of iterations in the correction. Default = 1.

## Details

Impulse indicator saturation results in an under-estimation of the error
variance as well as the variance of regressors not selected over. The
magnitude of the inconsistency increases with the p-value of selection
(`t.pval`). The function takes an
[`isat`](http://moritzschwarz.org/gets/reference/isat.md) object and
applies the impulse indicator consistency
([`isvarcor`](http://moritzschwarz.org/gets/reference/isvarcor.md)) and
efficiency correction
([`isvareffcor`](http://moritzschwarz.org/gets/reference/isvareffcor.md))
of the estimated error variance and the estimated variance of regressors
not selected over. See Johansen and Nielsen (2016a) and (2016b).

## Value

Returns an [`isat`](http://moritzschwarz.org/gets/reference/isat.md)
object in which the estimated standard errors, t-statistics, p-values,
standard error of the regression, and log-likelihood are consistency and
efficiency corrected when using impulse indicator saturation
(`iis=TRUE`).

## References

Johansen, S., & Nielsen, B. (2016a). Asymptotic theory of outlier
detection algorithms for linear time series regression models.
Scandinavian Journal of Statistics, 43(2), 321-348.

Johansen, S., & Nielsen, B. (2016b). Rejoinder: Asymptotic Theory of
Outlier Detection Algorithms for Linear. Scandinavian Journal of
Statistics, 43(2), 374-381.

Pretis, F., Reade, J., & Sucarrat, G. (2018). Automated
General-to-Specific (GETS) regression modeling and indicator saturation
methods for the detection of outliers and structural breaks. Journal of
Statistical Software, 86(3).

## Author

Felix Pretis, <https://felixpretis.climateeconometrics.org/>

## See also

[`isat`](http://moritzschwarz.org/gets/reference/isat.md),
[`isvarcor`](http://moritzschwarz.org/gets/reference/isvarcor.md),
[`isvareffcor`](http://moritzschwarz.org/gets/reference/isvareffcor.md)

## Examples

``` r
###Consistency and Efficiency Correction of Impulse Indicator Estimates
nile <- as.zoo(Nile)
isat.nile <- isat(nile, sis=FALSE, iis=TRUE, plot=TRUE, t.pval=0.1)
#> 
#> IIS block 1 of 4:
#> 9 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 4 
#> 5 
#> 6 
#> 7 
#> 8 
#> 9 
#> 
#> IIS block 2 of 4:
#> 23 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 4 
#> 5 
#> 6 
#> 7 
#> 8 
#> 9 
#> 10 
#> 11 
#> 12 
#> 13 
#> 14 
#> 15 
#> 16 
#> 17 
#> 18 
#> 19 
#> 20 
#> 21 
#> 22 
#> 23 
#> 
#> IIS block 3 of 4:
#> 24 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 4 
#> 5 
#> 6 
#> 7 
#> 8 
#> 9 
#> 10 
#> 11 
#> 12 
#> 13 
#> 14 
#> 15 
#> 16 
#> 17 
#> 18 
#> 19 
#> 20 
#> 21 
#> 22 
#> 23 
#> 24 
#> 
#> IIS block 4 of 4:
#> 25 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 4 
#> 5 
#> 6 
#> 7 
#> 8 
#> 9 
#> 10 
#> 11 
#> 12 
#> 13 
#> 14 
#> 15 
#> 16 
#> 17 
#> 18 
#> 19 
#> 20 
#> 21 
#> 22 
#> 23 
#> 24 
#> 25 
#> 
#> GETS of union of retained IIS variables... 
#> 
#> GETS of union of ALL retained variables...

isat.nile.corrected <- isatvarcorrect(isat.nile)

isat.nile$sigma2
#> [1] 13973.97
isat.nile.corrected$sigma2
#> [1] 22429.57
```
