# IIS Consistency Correction

Consistency correction for estimate of residual variance when using
impulse indicator saturation.

## Usage

``` r
isvarcor(t.pval, sigma)
```

## Arguments

- t.pval:

  numeric value. the p-value of selection in the impulse indicator
  saturation model.

- sigma:

  numeric value. The estimated standard deviation of the residuals from
  the impulse indicator saturation model.

## Value

a data frame containing the corrected standard deviation `$sigma.cor`
and the correction factor used `$corxi`

## Details

The Johansen and Nielsen (2016) impulse-indicator consistency correction
for the estimated residual standard deviation.

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
isvarcor(t.pval=0.05, sigma=2)
#>   sigma.cor    corxi
#> 1  2.295908 1.147954
```
