# Estimation of a log-variance model

Two-step estimation of a log-variance model: OLS in step 1, bias
correction w/residuals in step 2 (see the code for details). The
function `larchEstfun()` is not intended for the average user, but is
called by [`larch`](http://moritzschwarz.org/gets/reference/larch.md)
and
[`gets.larch`](http://moritzschwarz.org/gets/reference/gets.larch.md).

## Usage

``` r
larchEstfun(loge2, x, e, vcov.type = c("robust", "hac"), tol = 1e-07)
```

## Arguments

- loge2:

  numeric vector, the log of the squared errors 'e' (adjusted for zeros
  on e, if any)

- x:

  numeric matrix, the regressors

- e:

  numeric vector, the errors

- vcov.type:

  `character` vector, "robust" (default) or "hac". If "robust", then the
  White (1980) heteroscedasticity-robust variance-covariance matrix is
  used for inference. If "hac", then the Newey and West (1987)
  heteroscedasticity and autocorrelation-robust matrix is used

- tol:

  numeric value. The tolerance for detecting linear dependencies in the
  columns of the regressors in the first step estimation by OLS, see
  [`ols`](http://moritzschwarz.org/gets/reference/ols.md). Only used if
  `LAPACK` is `FALSE`

## Details

No details for the moment.

## Value

A [`list`](https://rdrr.io/r/base/list.html).

## References

No references for the moment.

## Author

Genaro Sucarrat, <http://www.sucarrat.net/>

## See also

[`qr`](https://rdrr.io/r/base/qr.html),
[`larch`](http://moritzschwarz.org/gets/reference/larch.md),
[`gets.larch`](http://moritzschwarz.org/gets/reference/gets.larch.md)

## Examples

``` r
##no examples for the moment
```
