# Estimate an autoregressive logit model with covariates

Estimate a dynamic Autoregressive (AR) logit model with covariates ('X')
by maximising the logit likelihood.

## Usage

``` r
logitx(y, intercept = TRUE, ar = NULL, ewma = NULL, xreg = NULL, 
    vcov.type = c("ordinary", "robust"), lag.length = NULL, 
    initial.values = NULL, lower = -Inf, upper = Inf, control = list(), 
    eps.tol = .Machine$double.eps, solve.tol = .Machine$double.eps,
    singular.ok = TRUE, plot = NULL)

dlogitx(y, ...)
```

## Arguments

- y:

  a binary numeric vector, time-series or
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) object. Missing values
  in the beginning and at the end of the series is allowed, as they are
  removed with the [`na.trim`](https://rdrr.io/pkg/zoo/man/na.trim.html)
  command

- intercept:

  logical. `TRUE`, the default, includes an intercept in the logit
  specification, whereas `FALSE` does not

- ar:

  either `NULL` (default) or an integer vector, say, `c(2,4)` or `1:4`.
  The AR-lags to include in the logit specification. If `NULL`, then no
  lags are included

- ewma:

  either `NULL` (default) or a
  [`list`](https://rdrr.io/r/base/list.html) with arguments sent to the
  [`eqwma`](http://moritzschwarz.org/gets/reference/eqwma.md) function.
  In the latter case a lagged moving average of `y` is included as a
  regressor

- xreg:

  either `NULL` (default) or a numeric vector or matrix, say, a
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) object, of covariates.
  Note that, if both `y` and `xreg` are
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) objects, then their
  samples are chosen to match

- vcov.type:

  character vector of length 1, either "ordinary" (default) or "robust".
  Partial matching is allowed. If "ordinary", then the ordinary
  variance-covariance matrix is used for inference. If "robust", then a
  robust coefficient-covariance of the Newey and West (1987) type is
  used

- lag.length:

  `NULL` or an integer that determines the lag-length used in the robust
  coefficient covariance. If `lag.length` is an integer, then it is
  ignored unless `method = 3`

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

- singular.ok:

  logical. If `TRUE` (default), then the regressors causing the
  singularity are dropped (using
  [`dropvar`](http://moritzschwarz.org/gets/reference/dropvar.md))
  before estimation. If `FALSE`, singularity returns error

- plot:

  `NULL` or logical. If `TRUE`, then a plot is produced. If `NULL`
  (default), then the value set by
  [`options`](https://rdrr.io/r/base/options.html) determines whether a
  plot is produced or not.

- ...:

  arguments passed on to `logitx`

## Details

The function estimates a dynamic Autoregressive (AR) logit model with
(optionally) covariates ('X') by maximising the logit likelihood. The
estimated model is an augmented version of the model considered by
Kauppi and Saikkonen (2008). Also, they considered estimation is by
maximisation of the probit likelihood. Here, by contrast, estimation is
by maximisation of the logit likelihood.

## Value

A list of class 'logitx'.

## References

Heikki Kauppi and Pentti Saikkonen (2008): 'Predicting U.S. Recessions
with Dynamic Binary Response Models'. The Review of Economics and
Statistics 90, pp. 777-791

Whitney K. Newey and Kenned D. West (1987): 'A Simple, Positive
Semi-Definite, Heteroskedasticity and Autocorrelation Consistent
Covariance Matrix', Econometrica 55, pp. 703-708

## Author

Genaro Sucarrat, <http://www.sucarrat.net/>

## See also

Methods:
[`coef.logitx`](http://moritzschwarz.org/gets/reference/coef.logitx.md),
[`fitted.logitx`](http://moritzschwarz.org/gets/reference/coef.logitx.md),
[`gets.logitx`](http://moritzschwarz.org/gets/reference/gets.logitx.md),  
[`logLik.logitx`](http://moritzschwarz.org/gets/reference/coef.logitx.md),
[`plot.logitx`](http://moritzschwarz.org/gets/reference/coef.logitx.md),
[`print.logitx`](http://moritzschwarz.org/gets/reference/coef.logitx.md),
[`summary.logitx`](http://moritzschwarz.org/gets/reference/coef.logitx.md),
[`toLatex.logitx`](http://moritzschwarz.org/gets/reference/coef.logitx.md)
and
[`vcov.logitx`](http://moritzschwarz.org/gets/reference/coef.logitx.md)  

Related functions:
[`logitxSim`](http://moritzschwarz.org/gets/reference/logitxSim.md),
[`logit`](http://moritzschwarz.org/gets/reference/logit.md),
[`nlminb`](https://rdrr.io/r/stats/nlminb.html)

## Examples

``` r
##simulate from ar(1):
set.seed(123) #for reproducibility
y <- logitxSim(100, ar=0.3)

##estimate ar(1) and store result:
mymod <- logitx(y, ar=1)

##estimate ar(4) and store result:
mymod <- logitx(y, ar=1:4)

##create some more data, estimate new model:
x <- matrix(rnorm(5*100), 100, 5)
mymod <- logitx(y, ar=1:4, xreg=x)
```
