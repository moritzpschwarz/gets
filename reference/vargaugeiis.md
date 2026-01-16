# Variance of the Impulse Indicator Saturation Gauge

Computes the variance of the gauge (false-positive rate of outliers
under the null of no outliers) in impulse indicator saturation based on
Jiao and Pretis (2019).

## Usage

``` r
vargaugeiis(t.pval, T, infty=FALSE, m=1)
```

## Arguments

- t.pval:

  numeric, between 0 and 1. Selection p-value used in indicator
  saturation.

- T:

  integer, sample sized used in indicator saturation.

- m:

  integer, number of iterations in variance computation, default=1

- infty:

  logical, argument used for variance computation

## Details

The function computes the variance of the Gauge (false-positive rate of
outliers in impulse indicator saturation) for a given level of
significance of selection (`t.pval`) and sample size (`T`) based on Jiao
and Pretis (2019). This is an auxilliary function used within the
[`outliertest`](http://moritzschwarz.org/gets/reference/outliertest.md)
function.

## Value

Returns a dataframe of the variance and standard deviation of the gauge,
as well the asymptotic variance and standard deviation.

## References

Jiao, X. & Pretis, F. (2019). Testing the Presence of Outliers in
Regression Models. Discussion Paper.

Pretis, F., Reade, J., & Sucarrat, G. (2018). Automated
General-to-Specific (GETS) regression modeling and indicator saturation
methods for the detection of outliers and structural breaks. Journal of
Statistical Software, 86(3).

## Author

Felix Pretis, <https://felixpretis.climateeconometrics.org/>

## See also

[`isat`](http://moritzschwarz.org/gets/reference/isat.md),
[`outliertest`](http://moritzschwarz.org/gets/reference/outliertest.md)

## Examples

``` r
  ###Computing the variance of the gauge under the null for a sample of T=200 observations:
  vargaugeiis(t.pval=0.05, T=200, infty=FALSE, m=1)
#>   var_iisgauge sd_iisgauge asy_var_iisgauge asy_sd_iisgauge
#> 1 0.0001062824  0.01030934       0.02125649       0.1457961
  
```
