# Sum and Sup Scaling Outlier Tests

Computes the Sum and Supremum Scaling Tests for the overall presence of
outliers based on Jiao and Pretis (2019).

## Usage

``` r
outlierscaletest(x, nsim = 10000)
```

## Arguments

- x:

  list, output of the
  [`isatloop`](http://moritzschwarz.org/gets/reference/isatloop.md)
  function

- nsim:

  integer, number of replications to simulate critical values for the
  Sup test

## Details

The function takes the output of the
[`isatloop`](http://moritzschwarz.org/gets/reference/isatloop.md)
function and computes the Scaling Sum and Supremum Tests for the
presence of outliers from Jiao and Pretis (2019). The test compares the
expected and observed proportion of outliers over the range of different
significance levels of selection specified in
[`isatloop`](http://moritzschwarz.org/gets/reference/isatloop.md). The
Sum test compares the sum of deviations against the standard normal
distribution, the Sup test compares the supremum of deviations against
critical values simulated with `nsim` replications. The null hypothesis
is that the observed proportion of outliers scales with the proportion
of outliers under the null of no outliers.

## Value

Returns a list of two `htest` objects. The first providing the results
of the Sum test on the sum of the deviation of outliers against a
standard normal distribution. The second providing the results on the
supremum of the deviation of outliers against simulated critical values.

## References

Jiao, X. & Pretis, F. (2019). Testing the Presence of Outliers in
Regression Models. Discussion Paper.

Pretis, F., Reade, J., & Sucarrat, G. (2018). Automated
General-to-Specific (GETS) regression modeling and indicator saturation
methods for the detection of outliers and structural breaks. Journal of
Statistical Software, 86(3).

## Author

Xiyu Jiao, & Felix Pretis,
<https://felixpretis.climateeconometrics.org/>

## See also

[`isat`](http://moritzschwarz.org/gets/reference/isat.md),
[`isatloop`](http://moritzschwarz.org/gets/reference/isatloop.md)

## Examples

``` r
  ###Repeated isat models using the Nile dataset
  ### where p-values are chosen such that the expected number of outliers under the null
  ### corresponds to 1, 2, ..., 20. Then computing the Outlier Scaling Tests:
  
  #nile <- as.zoo(Nile)
  #isat.nile.loop <- isatloop(y=nile)
  #outlierscaletest(isat.nile.loop)
  
```
