# IIS Efficiency Correction

Efficiency correction for the estimates of coefficient standard errors
on fixed regressors.

## Usage

``` r
isvareffcor(t.pval, se, m=1)
```

## Arguments

- t.pval:

  numeric value. the p-value of selection in the impulse indicator
  saturation model.

- se:

  numeric value or vector. The estimated standard errors of the
  coefficients on fixed regressors in impulse indicator saturation
  model.

- m:

  integer. The m-step correction factor.

## Value

a data frame containing the corrected standard deviation `$se.cor` and
the correction factor used `$eta.m`

## Details

The Johansen and Nielsen (2016) impulse-indicator efficiency correction
for the estimated standard errors on fixed regressors in impulse
indicator models.

## References

Johansen, S., & Nielsen, B. (2016): 'Asymptotic theory of outlier
detection algorithms for linear time series regression models.'
Scandinavian Journal of Statistics, 43(2), 321-348.

Pretis, Felix, Reade, James and Sucarrat, Genaro (2018): 'Automated
General-to-Specific (GETS) Regression Modeling and Indicator Saturation
for Outliers and Structural Breaks'. Journal of Statistical Software 86,
Number 3, pp. 1-44

## Author

Felix Pretis, <https://felixpretis.climateeconometrics.org/>

## See also

[`isatvar`](http://moritzschwarz.org/gets/reference/isatvar.md)

## Examples

``` r
isvareffcor(t.pval=0.05, se=2, m=1)
#>     se.cor    eta.m
#> 1 2.211732 1.105866
```
