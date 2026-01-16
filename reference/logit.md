# Estimation of a logit model

Maximum Likelihood (ML) estimation of a logit model.

## Usage

``` r
logit(y, x, initial.values = NULL, lower = -Inf, upper = Inf, 
    method = 2, lag.length = NULL, control = list(), eps.tol = .Machine$double.eps, 
    solve.tol = .Machine$double.eps )
```

## Arguments

- y:

  numeric vector, the binary process

- x:

  numeric matrix, the regressors

- initial.values:

  `NULL` or a numeric vector with the initial parameter values passed on
  to the optimisation routine,
  [`nlminb`](https://rdrr.io/r/stats/nlminb.html). If `NULL`, the
  default, then the values are chosen automatically

- lower:

  numeric vector, either of length 1 or the number of parameters to be
  estimated, see [`nlminb`](https://rdrr.io/r/stats/nlminb.html)

- upper:

  numeric vector, either of length 1 or the number of parameters to be
  estimated, see [`nlminb`](https://rdrr.io/r/stats/nlminb.html)

- method:

  an integer that determines the expression for the
  coefficient-covariance, see "details"

- lag.length:

  `NULL` or an integer that determines the lag-length used in the robust
  coefficient covariance. If `lag.length` is an integer, then it is
  ignored unless `method = 3`

- control:

  a `list` passed on to the control argument of
  [`nlminb`](https://rdrr.io/r/stats/nlminb.html)

- eps.tol:

  numeric, a small value that ensures the fitted zero-probabilities are
  not too small when the log-transformation is applied when computing
  the log-likelihood

- solve.tol:

  numeric value passed on to the `tol` argument of
  [`solve`](https://rdrr.io/r/base/solve.html), which is called whenever
  the coefficient-coariance matrix is computed. The value controls the
  toleranse for detecting linear dependence between columns when
  inverting a matrix

## Details

No details for the moment.

## Value

A [`list`](https://rdrr.io/r/base/list.html).

## References

No references for the moment.

## Author

Genaro Sucarrat, <http://www.sucarrat.net/>

## See also

[`nlminb`](https://rdrr.io/r/stats/nlminb.html),
[`solve`](https://rdrr.io/r/base/solve.html)

## Examples

``` r
##no examples for the moment
```
